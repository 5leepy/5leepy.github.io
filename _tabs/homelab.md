---
title: Homelab
icon: fas fa-server
order: 2
---

Di halaman ini saya catat *setup* **home lab** rumahan yang saya pakai sehari-hari — simpel, irit listrik, dan jalan di atas **laptop bekas** yang saya sulap jadi server Docker 24/7. Daripada beli perangkat *enterprise* yang mahal dan berisik, yang paling saya kejar di sini cuma tiga hal: stabil, gampang dirawat, dan serba otomatis.

---

## 🧱 Stack Layanan yang Lagi Jalan

Semua layanannya jalan di dalam *container* **Docker** pakai `docker-compose.yml` per *stack*, biar rapi, nggak saling ganggu, dan gampang kalau sewaktu-waktu mau dipindah atau di-*backup*.

### 1. Manajemen Container
* **[Dockge](https://github.com/louislam/dockge)** — manajer *stack* Docker Compose berbasis web yang enteng banget dan fokus langsung ke file `compose.yaml`. Saya suka Dockge karena nggak nyembunyiin konfigurasi di balik UI yang ribet; apa pun yang diubah di UI langsung kesimpan jadi file Compose standar yang gampang dibaca, diedit lewat terminal, atau di-*backup*.

### 2. Jaringan & DNS
* **[Pi-hole](https://pi-hole.net/)** — DNS *sinkhole* buat ngeblokir iklan dan *tracker* di satu jaringan rumah sekaligus. Begitu DNS rumah diarahkan ke Pi-hole, semua perangkat — dari laptop, HP, sampai Smart TV — langsung ke-cover tanpa perlu repot pasang ekstensi satu-satu.

### 3. Otomasi Media (*\*arr Stack*)
Biar urusan koleksi tontonan keluarga di rumah jalan otomatis, saya pasang ekosistem *\*arr* yang saling nyambung:
* **Prowlarr** — pusat *indexer* yang otomatis nyinkronin setting ke aplikasi *\*arr* lainnya.
* **Sonarr** — buat ngatur dan nyari serial TV secara otomatis.
* **Radarr** — sama kayak Sonarr, tapi khusus buat film.
* **Bazarr** — urusan download *subtitle* otomatis yang nyambung langsung ke Sonarr dan Radarr.
* **Jellyseerr** — halaman web yang rapi buat *request* film atau serial, jadi anggota keluarga di rumah tinggal klik aja.
* **qBittorrent** — *download client* utama yang terhubung ke alur kerja *\*arr* stack.

---

## 📐 Catatan Arsitektur & Pelajaran Penting

Salah satu pelajaran paling berharga pas ngoprek *media stack* di Docker itu soal **struktur folder dan *hardlink***.

Awalnya, saya misahin volume `/downloads` dan `/tv` atau `/movies` sebagai *bind mount* terpisah ke dalam *container*. Akibatnya, proses pindahin file jadi lemot banget karena sistem nganggep itu dua *filesystem* yang beda — jadinya harus *copy & delete*, bikin disk kerja keras dan makan *storage* dobel buat sementara.

Solusinya ternyata simpel: pakai **unified volume mount** di level *root* data (ngikutin saran dari TRaSH Guides), misalnya mapping satu folder induk `/data` yang isinya ada subfolder `torrents/` dan `media/`. Dengan satu titik *mount* yang sama di Sonarr, Radarr, dan qBittorrent:
* **Hardlink** langsung jalan instan tanpa makan ruang penyimpanan dua kali.
* Proses *atomic move* beres seketika pas file selesai di-download, jadi SSD/HDD laptop bekas nggak tersiksa.
* Urusan *permission* (`PUID/PGID`) juga jadi jauh lebih konsisten di semua *container*.

---

> Catatan ini bakal terus saya update kalau nanti ada layanan baru atau eksperimen ngoprek berikutnya di rumah.
