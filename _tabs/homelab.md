---
title: Homelab
icon: fas fa-server
order: 2
---

Di halaman ini saya catat *setup* **home lab** rumahan yang saya pakai sehari-hari — simpel, irit listrik, dan jalan di atas satu laptop bekas (`nadir-thinkpad`) yang saya sulap jadi server 24/7. Daripada beli perangkat *enterprise* yang mahal dan berisik, yang paling saya kejar di sini cuma tiga hal: stabil, gampang dirawat, dan serba otomatis.

Arsitekturnya bersifat **hybrid Windows + WSL2 (Debian 12)** di mesin yang sama: sebagian layanan jalan *native* di Windows (dengan penyimpanan media utama di `D:\Media`), sementara seluruh *container* Docker jalan rapi di dalam WSL2 Debian 12.

---

## 💻 Spesifikasi Hardware

| Komponen | Spesifikasi |
| :--- | :--- |
| **Perangkat** | **Lenovo ThinkPad E14 (Gen 1)** |
| **CPU** | **Intel Core i5-10210U** (4 Cores / 8 Threads, TDP 15W hemat daya) |
| **RAM** | **16 GB DDR4** |
| **Storage 1 (OS & Docker)** | **512 GB NVMe SSD** (`C:\` — Windows 11 Pro, WSL2, Docker, & repo kerja) |
| **Storage 2 (Media)** | **1 TB 2.5" SATA HDD** (`D:\Media` — pustaka Jellyfin & *\*arr stack*) |
| **Jaringan** | **1 Gbps Ethernet LAN** (koneksi utama server) + Wi-Fi 6 |
| **Daya** | Baterai internal berfungsi sebagai **UPS alami** saat listrik padam |

---

## 🧱 Stack Layanan yang Lagi Jalan

Untuk layanan berbasis *container*, semuanya jalan di **Docker** di dalam WSL2 pakai `docker-compose.yml` per *stack*, biar rapi, nggak saling ganggu, dan gampang kalau sewaktu-waktu mau dipindah atau di-*backup*.

### 1. Manajemen Container
* **[Dockge](https://github.com/louislam/dockge)** — manajer *stack* Docker Compose berbasis web yang enteng banget dan fokus langsung ke file `compose.yaml`. Saya suka Dockge karena nggak nyembunyiin konfigurasi di balik UI yang ribet; apa pun yang diubah di UI langsung kesimpan jadi file Compose standar yang gampang dibaca, diedit lewat terminal, atau di-*backup*.

### 2. Jaringan & DNS
* **[Pi-hole](https://pi-hole.net/)** — DNS *sinkhole* buat ngeblokir iklan dan *tracker* di satu jaringan rumah sekaligus. Begitu DNS rumah diarahkan ke Pi-hole, semua perangkat — dari laptop, HP, sampai Smart TV — langsung ke-cover tanpa perlu repot pasang ekstensi satu-satu.
* **[Tailscale](https://tailscale.com/)** — *mesh* VPN berbasis WireGuard buat akses aman jarak jauh antar perangkat, seperti laptop lain dan HP. Mau cek status server atau buka layanan rumah dari luar jaringan lokal tinggal nyalain Tailscale tanpa perlu repot buka *port forwarding* di router.

### 3. Media
* **[Jellyfin](https://jellyfin.org/)** — *media server* yang jalan *native* di Windows (port `8096`) dan langsung baca koleksi dari `D:\Media`. Semua film dan serial yang udah di-*download* langsung ke-indeks rapi lengkap dengan poster, sinopsis, dan *subtitle*, siap ditonton dari Smart TV, laptop, maupun HP.

### 4. Otomasi Media (*\*arr Stack*)
Biar urusan koleksi tontonan keluarga di rumah jalan otomatis, saya pasang ekosistem *\*arr* di Docker WSL2 yang saling nyambung:
* **Prowlarr** — pusat *indexer* yang otomatis nyinkronin setting ke aplikasi *\*arr* lainnya.
* **FlareSolverr** — *proxy server* pendamping buat ngebantu Prowlarr ngelewatin proteksi Cloudflare di beberapa *indexer*.
* **Sonarr** — buat ngatur dan nyari serial TV secara otomatis.
* **Radarr** — sama kayak Sonarr, tapi khusus buat film.
* **Bazarr** — urusan *download subtitle* otomatis yang nyambung langsung ke Sonarr dan Radarr.
* **Jellyseerr** — halaman web yang rapi buat *request* film atau serial, jadi anggota keluarga di rumah tinggal klik aja.
* **qBittorrent** — *download client* utama yang terhubung ke alur kerja *\*arr* stack.

---

## 📐 Catatan Arsitektur & Pelajaran Penting

Salah satu pelajaran paling berharga pas ngoprek *media stack* di Docker itu soal **struktur folder dan *hardlink***.

Awalnya, saya misahin volume `/downloads` dan `/tv` atau `/movies` sebagai *bind mount* terpisah ke dalam *container*. Akibatnya, proses pindahin file jadi lemot banget karena sistem nganggep itu dua *filesystem* yang beda — jadinya harus *copy & delete*, bikin disk kerja keras dan makan *storage* dobel buat sementara.

Solusinya ternyata simpel: pakai **unified volume mount** di level *root* data (ngikutin saran dari TRaSH Guides). Di *setup* ini, folder penyimpanan media di Windows (`D:\Media`) diakses dari WSL2 lewat `/mnt/d/Media`, lalu di-*mapping* jadi satu folder induk (misalnya ke `/data` di dalam *container*) yang isinya udah terstruktur buat kebutuhan *download* dan koleksi media buat dibaca Jellyfin. Dengan satu titik *mount* yang sama di Sonarr, Radarr, dan qBittorrent:
* **Hardlink** langsung jalan instan tanpa makan ruang penyimpanan dua kali.
* Proses *atomic move* beres seketika pas file selesai di-*download*, jadi disk laptop nggak tersiksa.
* Urusan *permission* (`PUID/PGID`) juga jadi jauh lebih konsisten di semua *container*.

---

> Catatan ini bakal terus saya update kalau nanti ada layanan baru atau eksperimen ngoprek berikutnya di rumah.
