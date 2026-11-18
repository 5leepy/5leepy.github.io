---
title: Homelab
icon: fas fa-server
order: 2
---

Halaman ini merangkum *setup* **home lab** rumahan yang saya jalankan sehari-hari — sederhana, hemat daya, dan dibangun di atas **laptop bekas** yang disulap menjadi server Docker 24/7. Alih-alih memakai perangkat *enterprise* yang mahal dan berisik, fokus utama saya di sini adalah keandalan, kemudahan pemeliharaan (*maintainability*), dan otomasi.

---

## 🧱 Stack Layanan Aktif

Seluruh layanan dijalankan dalam kontainer **Docker** menggunakan `docker-compose.yml` per *stack* agar tetap terisolasi dan mudah dipindahkan atau di-*backup*.

### 1. Manajemen Kontainer
* **[Dockge](https://github.com/louislam/dockge)** — manajer *stack* Docker Compose berbasis web yang ringan dan fokus pada file `compose.yaml`. Saya memilih Dockge karena ia tidak menyembunyikan konfigurasi di balik UI yang rumit; setiap perubahan di UI langsung tersimpan sebagai file Compose standar yang mudah dibaca, di-edit lewat terminal, atau di-backup.

### 2. Jaringan & DNS
* **[Pi-hole](https://pi-hole.net/)** — DNS *sinkhole* dan pemblokir iklan serta *tracker* untuk seluruh perangkat di jaringan rumah. Dengan memindahkan resolusi DNS ke Pi-hole di level jaringan, laptop, ponsel, hingga Smart TV di rumah otomatis terlindungi tanpa perlu memasang ekstensi di setiap perangkat.

### 3. Otomasi Media (*\*arr Stack*)
Untuk pengelolaan dan otomasi koleksi media rumah, saya menjalankan ekosistem *\*arr* yang saling terhubung:
* **Prowlarr** — pusat manajemen *indexer* yang menyinkronkan konfigurasi secara otomatis ke aplikasi *\*arr* lainnya.
* **Sonarr** — pelacakan dan otomasi serial TV.
* **Radarr** — pelacakan dan otomasi film.
* **Bazarr** — pengunduhan *subtitle* otomatis yang terintegrasi dengan Sonarr dan Radarr.
* **Jellyseerr** — antarmuka permintaan (*request*) media yang rapi dan ramah untuk anggota keluarga di rumah.
* **qBittorrent** — *download client* utama yang terhubung dengan alur kerja *\*arr* stack.

---

## 📐 Catatan Arsitektur & Pelajaran Penting

Salah satu pelajaran terbesar saat merancang *media stack* di Docker adalah soal **struktur direktori dan *hardlink***.

Awalnya, memisahkan volume `/downloads` dan `/tv` atau `/movies` sebagai *bind mount* terpisah ke dalam kontainer membuat proses pemindahan file berjalan lambat karena sistem menganggapnya sebagai dua *filesystem* berbeda (sehingga harus *copy & delete*, memakan I/O disk dan menggandakan pemakaian ruang sementara).

Solusinya adalah menerapkan **unified volume mount** di level *root* data (mengikuti prinsip dari TRaSH Guides), misalnya memetakan satu folder induk `/data` yang di dalamnya berisi subdirektori `torrents/` dan `media/`. Dengan satu titik *mount* yang sama di Sonarr, Radarr, dan qBittorrent:
* **Hardlink** bekerja secara instan tanpa memakan kapasitas penyimpanan ganda.
* Proses *atomic move* berjalan seketika saat file selesai diunduh, sehingga tidak membebani SSD/HDD laptop bekas.
* Izin akses (*PUID/PGID*) menjadi jauh lebih konsisten di seluruh kontainer.

---

> Catatan ini akan terus diperbarui seiring bertambahnya layanan baru atau eksperimen infrastruktur berikutnya di rumah.
