---
title: Setelah Install WSL, Apa Selanjutnya?
description: "Langkah awal setelah install WSL dan Ubuntu di Windows: cek versi WSL 2, update sistem, paham struktur folder Linux, akses file Windows, sampai error yang paling sering kejadian."
date: 2025-07-28 01:12:00 +0700
comments: true
categories: [Windows & WSL]
tags: [wsl, ubuntu, windows, terminal, linux, pemula]
media_subpath: /assets/img/posts/windows-guide/wsl-guide/
image:
  path: wsl-guide-thumbnail.webp
  lqip: data:image/webp;base64,UklGRtgAAABXRUJQVlA4IMwAAACQBwCdASp4AEEAP/3+/3+/uzUyJbtpc/A/iU3Fy7adZctv3P92llnh7x4B8iNzw+CEQg3k5k7F3gWrURgDdjIKPH9yRoAA/uPggBsdvt5UjEXVyrJpyFj805ADWW09n1Hi6Zm+G+FlTGf/nAhZuBJEHozHyvs9CfFIy6QTNEsnbfE+pK0/ks8Ff63zs69FLkp0Jl7P7XJy16gkrGkYLKfSXV7x/o5CGt9xRD20j0aZQFByghKIt1rAy5EOAS2DveYyld5Kctm2dEA0gAA=
  alt: "WSL siap digunakan — pelajari langkah berikutnya setelah instalasi Ubuntu di Windows."
---

Habis install WSL dan Ubuntu dari Microsoft Store, momen yang paling sering kejadian biasanya sama: layar hitam terminal kebuka, kursor kedip-kedip, lalu kepikiran, **“Terus ini ngapain?”**

Saya juga sempat begitu di awal. Supaya nggak bingung mau mulai dari mana, ini beberapa hal dasar yang paling berguna diberesin pertama kali: cek versi WSL, update paket, paham bedanya struktur folder Linux vs Windows, sampai jebakan kecil yang sering bikin pemula kaget.

---

## Update Sistem dan Pastikan Sudah WSL 2

Langkah pertama, pastikan dulu distro Linux kamu sudah jalan di **WSL 2** dan paket sistemnya nggak ketinggalan jauh.

### Cek versi WSL

Buka Windows Terminal (atau PowerShell), lalu jalankan:

```bash
wsl --version
```

Kalau muncul error, kemungkinan WSL di Windows kamu masih versi lama. Pastikan Windows 10 minimal versi 2004 dan fitur **Virtual Machine Platform** sudah aktif.

Kalau distromu ternyata masih di versi 1, pindahin ke versi 2 pakai perintah ini:

```bash
wsl --set-version <distro> 2
```

Contohnya untuk Ubuntu:

```bash
wsl --set-version Ubuntu 2
```

> WSL 2 pakai kernel Linux asli, jadi kompatibilitasnya (terutama buat Docker dan tool dev modern) jauh lebih aman dibanding WSL 1.
{: .prompt-info }

### Update Ubuntu

![Menjalankan update dan upgrade sistem di WSL](wsl-update-apt.png)
*Biasakan jalankan `sudo apt update && sudo apt upgrade` begitu selesai install distro baru.*

Lanjut perbarui daftar paket dan sistem Ubuntu-nya:

```bash
sudo apt update && sudo apt upgrade -y
```

> Flag `-y` dipakai supaya kita nggak perlu ketik `y` berkali-kali saat diminta konfirmasi upgrade.
{: .prompt-info }

---

## Struktur Folder & Navigasi Dasar

![Struktur filesystem Linux](wsl-folder-structure.png)
*Filesystem Linux dimulai dari root `/`, beda dengan Windows yang terpisah per huruf drive (`C:\`, `D:\`, dst).*

Perbedaan pertama yang paling kerasa pas pindah dari Windows ke Linux adalah cara susun foldernya. Di Linux nggak ada `C:\` atau `D:\`. Semuanya bernaung di bawah satu pohon direktori yang dimulai dari root `/`, lalu drive atau partisi lain di-*mount* ke subfolder di bawahnya.

Beberapa folder yang paling sering kamu temui:

* `/home/username` — folder pribadi kamu, mirip `C:\Users\namakamu` di Windows.
* `/etc` — tempat simpan file konfigurasi sistem dan aplikasi.
* `/bin`, `/usr/bin`, `/sbin` — lokasi file binary program dan perintah.
* `/mnt` — tempat drive Windows muncul dan bisa diakses dari WSL.

### Navigasi Dasar di Terminal

Nggak perlu hafal banyak perintah dulu. Cukup biasain enam ini dulu:

```bash
pwd          # Cek kamu lagi ada di folder mana
ls           # Lihat isi folder
cd <folder>  # Masuk ke folder tertentu
cd ..        # Naik satu tingkat ke folder sebelumnya
cd ~         # Balik cepat ke folder home
clear        # Bersihkan layar terminal
```

### Bikin dan Hapus Folder

```bash
mkdir nama_folder         # Bikin folder baru
rmdir nama_folder         # Hapus folder kosong
rm -r nama_folder         # Hapus folder beserta seluruh isinya
```

> Biasakan tekan `Tab` buat auto-complete nama folder biar nggak capek ngetik dan jarang typo. `Ctrl + L` juga bisa dipakai sebagai pengganti `clear`.
{: .prompt-tip }

---

## Akses File Windows dari Linux (WSL)

![Akses folder Windows dari dalam WSL](wsl-access-windows-folder.png)
*Drive Windows otomatis muncul di bawah `/mnt/c`, `/mnt/d`, dan seterusnya.*

Semua drive Windows bisa langsung kamu buka dari dalam WSL lewat folder `/mnt`. Misalnya mau masuk ke folder Downloads Windows:

```bash
cd /mnt/c/Users/nama_kamu/Downloads
```

### Catatan Penting: Hati-Hati Edit File Linux dari Aplikasi Windows

Dari Windows Explorer kamu memang bisa ngintip isi folder Linux lewat `\\wsl$`. Tapi biasakan **jangan mengedit atau memindahkan file internal Linux langsung pakai aplikasi Windows klasik** seperti Notepad biasa.

> Edit file Linux dari sisi Windows kadang bisa bikin *permission* atau *line ending* (CRLF vs LF) berantakan, dan di kasus tertentu bikin script Linux gagal jalan. Kalau mau edit file di dalam WSL, pakai `nano`, `vim`, atau buka lewat `code .` pakai ekstensi WSL di VS Code.
{: .prompt-warning }

### Buka Aplikasi Windows dari Terminal Linux

Uniknya WSL, kamu juga bisa manggil executable Windows langsung dari terminal Linux:

* Buka folder saat ini di File Explorer:

```bash
explorer.exe .
```

Ini enak buat sekadar ngecek atau mindahin file hasil download, tapi tetap hindari edit file konfigurasi Linux lewat sana.

> Kalau mau folder bersama yang aman diakses bolak-balik antara Windows dan Linux, taruh di area Windows (`/mnt/c/Users/...`). Tapi untuk repo koding (`git`, `node_modules`), tetap simpan di `/home/username` biar nggak lemot.
{: .prompt-info }

* Buka file teks cepat di Notepad:

```bash
notepad.exe file.txt
```

* Buka folder proyek di VS Code:

```bash
code .
```

> Pastikan VS Code dan ekstensi WSL sudah terpasang di Windows.
{: .prompt-info }

---

## Shortcut Terminal yang Kepake Tiap Hari

Kalau udah mulai sering ngetik di terminal, lima shortcut ini jauh lebih ngirit waktu dibanding pakai tombol panah atau Backspace terus-terusan:

> 🔧 **Shortcut Harian**
>
> * `Ctrl + L` → Bersihkan layar
> * `Ctrl + A` → Lompat ke awal baris
> * `Ctrl + E` → Lompat ke akhir baris
> * `Ctrl + U` → Hapus seluruh teks dari posisi kursor ke awal baris
> * `Ctrl + R` → Cari perintah lama dari riwayat (ketik potongan katanya aja)

> Tombol panah atas dan bawah juga tetap bisa dipakai buat mundur-maju ke perintah sebelumnya.
{: .prompt-info }

---

## Cek Dokumentasi Langsung di Terminal

![Menggunakan perintah man untuk melihat dokumentasi ls](wsl-man-ls.png)
*Menjalankan `man ls` untuk membuka halaman manual langsung di terminal.*

Jujur aja, di praktik sehari-hari sekarang kebanyakan orang lebih sering cek `--help` atau langsung cari di browser kalau lupa opsi perintah. Tapi tahu cara pakai `man` tetap berguna, terutama pas lagi nggak ada internet atau butuh lihat daftar flag lengkap dari sebuah tool.

### Perintah `man`

```bash
man <nama_perintah>
```

Contoh:

```bash
man ls
```

> Hal paling penting pas pertama kali buka `man`: tekan tombol **`q`** buat keluar. Banyak pemula sempat bingung atau panik karena `Ctrl + C` nggak ngaruh di halaman `man`.
{: .prompt-tip }

### Alternatif yang Lebih Ringkas

* `--help` — ini yang paling sering saya pakai sehari-hari karena output-nya langsung to the point:

```bash
ls --help
```

* `whatis <perintah>` — cek deskripsi satu baris dari sebuah perintah:

```bash
whatis grep
```

* `apropos <kata>` — cari perintah berdasarkan kata kunci kalau lupa nama persisnya:

```bash
apropos network
```

---

## Kenali Beberapa Flag Umum

Di Linux, opsi perintah biasanya ditulis pakai tanda minus (`-`). Tiga yang paling sering ketemu di awal:

* `-y` : jawab "yes" otomatis
* `-r` : recursive (berlaku ke folder beserta seluruh isinya)
* `-f` : force (paksa jalan tanpa tanya lagi)

Contoh gabungannya:

```bash
sudo rm -rf folderku
```

> Hati-hati banget sama `rm -rf`. Di Linux nggak ada Recycle Bin — begitu kepencet Enter, isi foldernya langsung hilang tanpa konfirmasi.
{: .prompt-danger }

---

## Beberapa Error yang Paling Sering Muncul di Awal

### ❌ `Command not found`

Biasanya cuma dua kemungkinan: salah ketik, atau paketnya memang belum terpasang.

```bash
sudo apt install nama-paket
which nama-perintah
```

### 🔒 `Permission denied`

![Contoh error permission di WSL](wsl-permission-error.png)
*Error `Permission denied` muncul saat akun biasa mencoba mengakses atau mengubah file yang butuh hak akses lebih tinggi.*

Kalau memang perintahnya butuh hak admin (seperti install paket atau edit file di `/etc`), tambahkan `sudo` di depan. Kalau urusannya file biasa, cek dulu kepemilikan dan izin filenya:

```bash
ls -l
```

### 📂 Folder Windows nggak ketemu

Kalau path `/mnt/c/...` error:

* Cek lagi huruf besar-kecilnya — Linux itu **case-sensitive**, jadi `Downloads` dan `downloads` dianggap beda.
* Jalankan `ls /mnt` untuk memastikan drive-nya memang sudah ter-mount.

---

## Sekilas soal Ganti Shell: Bash vs Zsh

Secara default, Ubuntu di WSL memakai **Bash**. Buat kebutuhan harian, scripting, dan navigasi dasar, Bash sebenarnya udah sangat cukup dan nggak ada kewajiban buat ganti.

Tapi kalau nanti kamu udah mulai nyaman dan pengen pengalaman terminal yang lebih enak dipakai ngetik cepat, banyak orang pindah ke **Zsh** (biasanya dipasangkan dengan `oh-my-zsh`). Beberapa alasan umumnya:

* **Auto-complete lebih enak:** saran folder dan argumen perintahnya lebih kontekstual.
* **Koreksi typo:** salah ketik perintah kadang langsung dikasih saran pembenaran.
* **Tema & plugin melimpah:** gampang nambahin status Git, syntax highlighting, sampai autosuggestions dari history.

Selain Zsh, ada juga **Fish** yang fitur auto-complete dan warna-warnanya sudah jalan enak dari bawaan tanpa banyak setting, cuma sintaks scripting-nya sedikit beda dari Bash.

> Nggak perlu buru-buru ganti shell di hari pertama. Biasakan dulu kerja di Bash sampai ritme terminalnya kerasa natural, baru nanti eksplor Zsh atau kustomisasi prompt.
{: .prompt-info }

---

## Penutup

Sampai titik ini, kamu udah pegang bekal utama buat mulai kerja di WSL: sistem sudah update di WSL 2, paham bedanya folder Linux dan Windows, tahu shortcut harian, dan nggak kaget lagi kalau ketemu error standar kayak `Permission denied`.

Dari sini, cara paling cepat biar makin lancar ya langsung dipakai buat kerjaan nyata — entah buat `git`, jalanin project lokal, atau nyoba Docker.

> **Seri Panduan Windows & WSL:**
> 1. [Bagian 1: Mengenal Windows Terminal](/posts/windows-terminal-cli/)
> 2. [Bagian 2: Mengenal WSL di Windows](/posts/wsl-di-windows/)
> 3. **Bagian 3: Setelah Install WSL, Apa Selanjutnya?** *(kamu di sini)*
{: .prompt-info }
