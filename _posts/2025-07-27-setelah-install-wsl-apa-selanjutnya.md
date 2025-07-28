---
title: Setelah Install WSL, Apa Selanjutnya?
description: Panduan singkat dan praktis untuk pengguna baru WSL setelah instalasi. Pelajari struktur direktori, perintah penting, dan cara menyesuaikan lingkungan shell Linux di Windows.
date: 2025-07-28 01:12:00 +0700
comments: true
categories: [Panduan, WSL]
tags: [wsl, ubuntu, windows, terminal, linux, pemula]
media_subpath: /windows-guide/wsl-guide/
image:
  path: wsl-guide-thumbnail.webp
  lqip: data:image/webp;base64,UklGRtgAAABXRUJQVlA4IMwAAACQBwCdASp4AEEAP/3+/3+/uzUyJbtpc/A/iU3Fy7adZctv3P92llnh7x4B8iNzw+CEQg3k5k7F3gWrURgDdjIKPH9yRoAA/uPggBsdvt5UjEXVyrJpyFj805ADWW09n1Hi6Zm+G+FlTGf/nAhZuBJEHozHyvs9CfFIy6QTNEsnbfE+pK0/ks8Ff63zs69FLkp0Jl7P7XJy16gkrGkYLKfSXV7x/o5CGt9xRD20j0aZQFByghKIt1rAy5EOAS2DveYyld5Kctm2dEA0gAA=
  alt: "WSL siap digunakan — pelajari langkah berikutnya setelah instalasi Ubuntu di Windows."
---

WSL (Windows Subsystem for Linux) adalah cara praktis untuk menjalankan Linux di dalam Windows tanpa harus dual-boot. Tapi setelah install Ubuntu dari Microsoft Store, banyak pengguna bingung: **“Selanjutnya ngapain?”**

Artikel ini akan membimbingmu langkah demi langkah setelah install WSL: dari pembaruan sistem, memahami struktur folder Linux dan akses file Windows, hingga mempercantik terminal menggunakan Zsh dan Oh My Posh.

---

## Update Sistem dan Pahami Versi WSL

Setelah instalasi, langkah pertama yang perlu kamu lakukan adalah memastikan sistem WSL dan distro Linux-mu up-to-date serta berjalan di versi terbaiknya: WSL 2.

### Cek versi WSL:

Pertama, buka Windows Terminal (atau bisa juga lewat CMD/PowerShell), lalu jalankan:

```bash
wsl --version
```

Jika muncul pesan error, kemungkinan kamu masih menggunakan WSL versi lama (legacy). Untuk memastikan kamu bisa menggunakan WSL 2, pastikan kamu sudah update Windows 10 minimal versi 2004 dan mengaktifkan fitur “Virtual Machine Platform”.

Jika distromu belum menggunakan WSL 2, kamu bisa ubah dengan perintah berikut:

```bash
wsl --set-version <distro> 2
```

Contoh:

```bash
wsl --set-version Ubuntu 2
```

> Mengapa perlu WSL 2? Versi ini menawarkan kinerja yang jauh lebih baik dan kompatibilitas penuh dengan kernel Linux, menjadikannya pilihan ideal untuk pengembangan. Pastikan distromu sudah di WSL 2 untuk pengalaman terbaik.
{: .prompt-info }

### Update Ubuntu:

![Menjalankan update dan upgrade sistem di WSL](wsl-update-apt.png)
*Perintah `sudo apt update && sudo apt upgrade` digunakan untuk memastikan sistem Linux kamu tetap up-to-date di WSL.*

Setelah memastikan WSL berjalan dengan versi 2, waktunya memperbarui sistem Ubuntu-mu.

```bash
sudo apt update && sudo apt upgrade -y
```

> `-y` berarti kamu menyetujui semua prompt "yes" agar proses upgrade otomatis.
{: .prompt-info }
---

## Struktur Folder & Navigasi Dasar

![Struktur filesystem Linux](wsl-folder-structure.png)
*Struktur filesystem Linux dimulai dari root `/`, tidak seperti Windows yang terpisah per drive (`C:\`, `D:\`, dll).*

Di Linux, semua dimulai dari direktori root `/`. Bayangkan ini seperti **drive C:** di Windows. Namun, berbeda dengan Windows yang memisahkan drive (C:, D:, E:), Linux "memasang" (mount) semua drive dan perangkat di bawah satu pohon direktori, dimulai dari root.

Contohnya:

* `/home/username` adalah tempat file pribadi kamu, mirip dengan `C:\Users\namakamu` di Windows.
* `/etc` berisi file konfigurasi sistem.
* `/bin`, `/usr/bin`, dan `/sbin` adalah lokasi program dan perintah.
* `/mnt` atau `/media` digunakan untuk mengakses drive eksternal yang kamu mount dari Windows.

### Navigasi Dasar di Terminal

Gunakan terminal Linux di dalam WSL untuk berpindah dan mengeksplorasi folder:

```bash
pwd          # Menampilkan direktori saat ini
ls           # Melihat isi folder
cd <folder>  # Masuk ke folder tertentu
cd ..        # Kembali ke folder sebelumnya
cd ~         # Pergi ke folder home
clear        # bersihkan layar
```

### Membuat dan Menghapus Folder

Selain navigasi, kamu juga bisa membuat dan menghapus folder:

```bash
mkdir nama_folder         # Membuat folder baru
rmdir nama_folder         # Menghapus folder kosong
rm -r nama_folder         # Menghapus folder beserta isinya
```

> Gunakan `Tab` untuk melengkapi nama folder otomatis saat mengetik, dan `Ctrl + L` untuk membersihkan layar terminal.
{: .prompt-tip }
---

## Akses File Windows dari Linux (WSL)

![Akses folder Windows dari dalam WSL](wsl-access-windows-folder.png)
*Di WSL, kamu bisa mengakses file Windows melalui `/mnt/c`, `/mnt/d`, dst.*

Salah satu keunggulan WSL adalah kamu bisa mengakses file Windows langsung dari dalam Linux. File sistem Windows tersedia di direktori `/mnt`, dan tiap drive memiliki subfolder tersendiri:

Contoh:

```bash
cd /mnt/c/Users/nama_kamu/Downloads
```

Ini akan membawamu ke folder **Downloads** di drive C: milik Windows.

### Peringatan Penting: Jangan Edit File Linux dari Windows

WSL juga memungkinkan kamu mengakses file Linux dari Windows Explorer, tapi **jangan pernah mengedit file Linux menggunakan aplikasi Windows** (misalnya Notepad atau VS Code dari Windows), apalagi memindahkan file Linux lewat File Explorer.

**Mengapa?**
> Karena mengedit file Linux dari Windows Explorer bisa merusak metadata file Linux dan menyebabkan korupsi filesystem. Selalu lakukan pengeditan dari dalam terminal WSL menggunakan editor seperti `nano`, `vim`, atau `code .` (jika menggunakan VS Code WSL extension).
{: .prompt-warning }

### Jalankan Aplikasi Windows dari Linux

* Kamu bisa membuka Windows File Explorer dari dalam WSL dengan mengetik:

```bash
explorer.exe .
```

* Ini akan membuka direktori saat ini dalam File Explorer, tapi tetap gunakan ini **hanya untuk melihat**, bukan mengedit file Linux.

> Jika ingin berbagi file antara Windows dan Linux, simpan file tersebut di direktori `/mnt/c/Users/...`, yaitu di area Windows yang aman untuk diakses dari kedua sistem.
{: .prompt-info }

* Edit teks:

```bash
notepad.exe file.txt
```

* Buka folder di VS Code:

```bash
code .
```

> Pastikan VS Code dan ekstensi WSL sudah terinstal.
{: .prompt-info }

---

## Shortcut Terminal Linux yang Perlu Kamu Tahu

> 🔧 **Tips Navigasi Cepat**
>
> * `Ctrl + L` → Clear layar
> * `Ctrl + A` → Ke awal baris
> * `Ctrl + E` → Ke akhir baris
> * `Ctrl + U` → Hapus baris dari awal
> * `Ctrl + R` → Cari perintah sebelumnya

> Gunakan tombol panah atas dan bawah untuk navigasi riwayat perintah.
{: .prompt-info }
---

## Gunakan Dokumentasi Internal Linux

![Menggunakan perintah man untuk melihat dokumentasi ls](wsl-man-ls.png)
*Gunakan `man ls` untuk membuka dokumentasi lengkap perintah `ls`—seperti ensiklopedia mini langsung di terminalmu.*


Linux dilengkapi dengan dokumentasi bawaan yang sangat berguna. Perintah `man` (manual) adalah alat utama untuk memahami cara kerja perintah di Linux.

### Perintah man

```bash
man <nama_perintah>
```

Contoh:

```bash
man ls
```

Ini akan membuka halaman manual untuk perintah `ls`.

> Bayangkan `man` seperti **ensiklopedia mini di terminalmu**. Jika kamu bingung dengan opsi sebuah perintah, `man` akan menampilkan semua detailnya—dari penjelasan singkat hingga daftar lengkap parameter dan cara penggunaan.
{: .prompt-info }

### Perintah lain yang berguna:

* `--help`: Hampir semua perintah memiliki opsi ini untuk melihat ringkasan cepat.

```bash
ls --help
```

* `whatis <perintah>`: Menampilkan deskripsi singkat tentang perintah.

```bash
whatis grep
```

* `apropos <kata>`: Mencari perintah berdasarkan kata kunci.

```bash
apropos network
```

> Tip: Jika halaman `man` terlalu panjang, gunakan tombol panah atau `q` untuk keluar.
{: .prompt-tip }

---

## Kenali Flag Umum Linux

Contoh flag:

* `-y` : jawab "yes" otomatis
* `-r` : recursive (misalnya menghapus folder beserta isinya)
* `-f` : force (paksa, abaikan error)

Contoh kombinasi:

```bash
sudo rm -rf folderku
```

> Hati-hati! Perintah ini bisa menghapus semua isi folder tanpa konfirmasi.
{: .prompt-danger }
---

## Beberapa Masalah Umum

### ❌ Command not found

**Penyebab:** salah ketik atau belum terinstal

**Solusi:**

```bash
sudo apt install nama-paket
which nama-perintah
```

### 🔒 Permission denied

![Contoh error permission di WSL](wsl-permission-error.png)
*Contoh error <code>Permission denied</code> di WSL saat mencoba mengakses direktori tanpa hak yang sesuai. Solusinya? Gunakan <code>sudo</code> atau pastikan kamu punya izin akses.*

**Solusi:** Tambahkan `sudo` atau periksa hak akses:

```bash
ls -l
```

### 📂 Tidak bisa akses folder Windows

**Solusi:**

* Pastikan jalur `/mnt/c/...` benar
* Gunakan `ls /mnt` untuk melihat apakah drive ter-mount

---

## Saatnya Upgrade Terminal-mu

WSL biasanya menggunakan **Bash** sebagai shell default. Bash adalah fondasi yang kokoh dalam dunia Linux, dan sudah lebih dari cukup untuk kebutuhan dasar scripting, navigasi sistem, dan otomasi.

Namun, banyak pengguna memilih **Zsh (Z Shell)** karena beberapa alasan menarik:

* **Autokomplet Lebih Canggih:** Zsh bisa menampilkan saran lengkap dan kontekstual saat kamu mulai mengetik.
* **Koreksi Otomatis:** Salah ketik `grpe`? Zsh bisa menyarankan "maksudmu grep?".
* **Kustomisasi Visual:** Dengan framework seperti `oh-my-zsh`, kamu bisa menambahkan tema, plugin, dan tampilan terminal yang modern dan informatif.
* **Fitur Tambahan:** Seperti globbing yang lebih powerful dan navigasi history yang lebih fleksibel.

Selain Zsh, ada juga shell lain seperti **Fish** (Friendly Interactive SHell) yang lebih ramah pemula dan modern.

> Di artikel lanjutan, kita akan membahas cara mengganti shell dan memaksimalkannya dengan tema dan plugin.
{: .prompt-info }
---

## Siap Lanjut ke Level Berikutnya

Sekarang kamu sudah siap menggunakan WSL dengan lebih percaya diri: tahu cara update sistem, navigasi folder, akses file Windows, dan mengatasi masalah umum.

Ini baru permulaan. Terminal yang fungsional itu bagus—tapi terminal yang canggih dan indah? Jauh lebih seru. Sampai ketemu di panduan berikutnya!
