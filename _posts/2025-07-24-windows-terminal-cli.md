---
title: "Mengenal Windows Terminal: Satu Jendela untuk Semua Shell di Windows"
description: "Kenalan dengan Windows Terminal, pengganti CMD dan PowerShell klasik yang bikin kerja di baris perintah Windows jauh lebih rapi dan nyaman dipakai harian."
date: 2025-07-24 22:00:00 +0700
comments: true
categories: [Windows & WSL]
tags: [windows, terminal, cli, powershell, wsl, productivity]
media_subpath: /assets/img/posts/windows-guide/win-terminal/
image:
  path: terminal-thumbnail.webp
  lqip: data:image/webp;base64,UklGRrQAAABXRUJQVlA4IKgAAAAwBgCdASoyABsAP6HC2V86Mq0lLBqsy0A0CWwAvvxOVhw/o+TLbKZB7IW04KGPnGq5S6YqTNgs8Oj+AP68ckjgsjgnwSCsOgfPASiqixN8/Xt86VGtWI6ax+bFjdG0tbRYeplPLq7p3FPHAZT1dG0ROcweM20PMP1wLZSs0JXwYAyJ1Otnr46vdK5RtI7gPS86/Vc1q0Z6ZagqYGoaHPwuJM3bnB4fgAA=
  alt: "Mulai kenal Windows Terminal: satu aplikasi untuk PowerShell, CMD, WSL, dan lebih banyak lagi."
---

Kalau kamu sering kerja di Windows dan sesekali buka CMD, PowerShell, Git Bash, atau WSL, pasti pernah ngerasain layar desktop cepat penuh sama jendela terminal yang terpisah-pisah. Dulu saya juga gitu — baru buka dua-tiga sesi aja udah bingung nyari mana jendela yang mana.

Di situlah **Windows Terminal** kerasa banget bedanya. Microsoft pertama kali ngerilis aplikasi ini di 2019 untuk menggantikan pengalaman konsol klasik di Windows. Intinya sederhana: PowerShell, Command Prompt, WSL (Windows Subsystem for Linux), Git Bash, sampai sesi SSH bisa dibuka semua dari satu aplikasi yang sama.

![Tampilan Windows Terminal dengan beberapa tab aktif](windows-terminal-tabs.png)
*Beberapa shell sekaligus — PowerShell, CMD, sampai WSL — cukup dibuka dalam satu jendela tab.*

## Kenapa Masih Pakai Terminal?

Buat sebagian orang, terminal kelihatan kuno dibanding aplikasi GUI. Tapi begitu udah terbiasa, ada beberapa pekerjaan yang memang jauh lebih cepat selesai lewat baris perintah:

* Menjalankan otomasi lewat script untuk kerjaan yang berulang
* Eksekusi perintah cepat tanpa harus klik menu berlapis-lapis
* Cek dan atur sistem lebih dalam dibanding tampilan Settings biasa
* Menjalankan tool harian berbasis teks seperti `git`, `curl`, atau `ffmpeg`

Di Windows sendiri, PowerShell biasanya jadi andalan kalau butuh scripting dan manajemen sistem. Contoh perintah dasarnya:

```powershell
Get-Process          # Melihat proses yang berjalan
Get-Service          # Melihat status service
Get-ChildItem        # Sama seperti ls/dir
Set-ExecutionPolicy  # Mengatur hak eksekusi script
```

> Buat urusan administrasi sistem atau otomasi di Windows, PowerShell jauh lebih fleksibel dibanding CMD klasik.
{: .prompt-info }

## Apa Bedanya dengan CMD dan PowerShell Klasik?

Kalau dilihat daftar fiturnya memang banyak. Dari pemakaian harian saya, ini beberapa hal yang paling kerasa manfaatnya (plus sedikit catatan kecil di praktiknya):

### 1. **Multiple Tabs**

Ini alasan utama kenapa saya langsung pindah dari konsol bawaan. Cara kerjanya persis kayak tab di browser: satu tab buat PowerShell, sebelahnya Ubuntu di WSL, satu lagi buat SSH ke mesin lain. Taskbar jadi jauh lebih bersih.

> Gunakan `Ctrl+Shift+T` untuk membuka tab baru.
{: .prompt-tip }

### 2. **Split Panes**

![Split panes horizontal dan vertikal di Windows Terminal](windows-terminal-split-panes.png)
*Split panes kepake banget kalau lagi mantau log di satu sisi sambil jalankan perintah di sisi lain.*

Layar satu tab bisa dibagi jadi beberapa panel, horizontal atau vertikal. Buat saya ini paling kepake saat lagi jalanin server lokal atau mantau log di panel kiri, sambil ngetik perintah `git` atau tes `curl` di panel kanan.

> Shortcut default: `Alt+Shift+-` untuk split horizontal, `Alt+Shift++` untuk split vertikal.
{: .prompt-tip }

### 3. **Profiles untuk Semua Shell**

![Menu profiles di Windows Terminal](windows-terminal-profiles.png)
*Tiap shell punya profil sendiri, lengkap dengan ikon, font, dan folder awal.*

Begitu kamu install Git Bash atau distro Linux di WSL, Windows Terminal biasanya otomatis mendeteksi dan menambahkannya ke daftar profil. Kamu bisa ngatur:

* PowerShell
* CMD
* Git Bash
* Ubuntu / Debian via WSL
* Azure CLI
* Koneksi SSH tertentu

Enaknya, masing-masing profil bisa dibedakan warna atau ikonnya, jadi nggak gampang salah ketik perintah Linux di tab PowerShell.

### 4. **Kustomisasi Tampilan**

Windows Terminal cukup fleksibel urusan tampilan:

* Tema gelap dan terang
* Font monospace modern seperti Cascadia Code atau Nerd Font
* Efek transparan / akrilik
* Skema warna sendiri

![Contoh pengaturan tampilan tema](windows-terminal-themes.png)
*Pengaturan tema, font, dan skema warna bisa diubah langsung dari menu Settings.*

Catatannya: efek transparan atau akrilik memang kelihatan keren buat screenshot, tapi di pemakaian lama kadang bikin teks agak susah dibaca kalau wallpaper di belakangnya terang. Saya pribadi biasanya pakai background solid gelap dengan font yang agak gedean biar mata nggak cepat capek.

> Sekarang hampir semua pengaturan bisa diubah lewat menu **Settings** (`Ctrl+,`). File `settings.json` tetap bisa diedit langsung kalau mau *copy-paste* konfigurasi antar mesin.
{: .prompt-info }

> Kalau ngedit `settings.json` secara manual, pastikan format JSON-nya valid. Salah satu koma aja bisa bikin konfigurasi gagal dimuat.
{: .prompt-warning }

### 5. **Dukungan Unicode dan UTF-8**

Di CMD lama, karakter khusus, simbol panah, atau ikon dari prompt modern sering tampil jadi kotak-kotak berantakan. Di Windows Terminal, dukungan Unicode dan UTF-8 udah jauh lebih rapi, jadi nyaman dipakai bareng tool modern yang banyak pakai ikon atau emoji di output-nya.

### 6. **Quake Mode dan Command Palette**

* **Quake Mode**: tekan `` Win + ` `` (backtick, default di layout keyboard US; di layout lain tombolnya bisa beda) untuk memunculkan terminal drop-down dari atas layar. Praktis kalau cuma mau cek cepat tanpa pindah jendela — walaupun di awal kadang suka kaget kalau nggak sengaja kepencet.

![Quake Mode aktif di Windows Terminal](windows-terminal-quake.png)
*Quake Mode muncul dari atas layar lewat `` Win + ` `` (keyboard US).*

* **Command Palette**: tekan `Ctrl+Shift+P` untuk nyari dan jalanin perintah Windows Terminal, mirip kayak di VS Code. Kepake banget kalau lupa shortcut split pane atau ganti skema warna.

![Command Palette di Windows Terminal](windows-terminal-command.png)
*Command Palette membantu cari fitur tanpa harus hafal semua shortcut.*

> Ada juga **Focus Mode** kalau kamu mau tampilan fullscreen yang bersih tanpa tab bar.
{: .prompt-info }

### 7. **Rendering Teks Lebih Halus**

Windows Terminal memakai GPU rendering (DirectWrite/DirectX). Efeknya kelihatan pas lagi jalanin perintah yang nge-print ribuan baris log — scroll-nya jauh lebih mulus dan nggak patah-patah kayak CMD lama.

> Jalankan terminal sebagai Administrator hanya kalau memang butuh. Menjalankan script sembarangan dengan hak admin risikonya lumayan besar.
{: .prompt-danger }

## Cara Install Windows Terminal

Di Windows 11 versi baru, Windows Terminal biasanya sudah terpasang bawaan. Kalau di mesinmu belum ada, cara paling gampangnya lewat Microsoft Store:

![Halaman Windows Terminal di Microsoft Store](terminal-store.png)
*Windows Terminal bisa diunduh langsung dari Microsoft Store.*

1. Buka **Microsoft Store**
2. Cari “Windows Terminal”
3. Klik **Install**

> Versi Microsoft Store biasanya paling praktis karena dapet update otomatis tanpa perlu urus manual.
{: .prompt-tip }

Kalau lebih suka lewat command line, bisa pakai dua cara ini:

### Menggunakan `winget`

```powershell
winget install --id Microsoft.WindowsTerminal -e
```

### Menggunakan PowerShell (untuk Windows 10/11)

```powershell
Invoke-WebRequest -Uri https://aka.ms/terminal -OutFile Terminal.msixbundle
Add-AppxPackage .\Terminal.msixbundle
```

> Untuk instalasi manual `.msixbundle`, pastikan Developer Mode atau sideloading apps sudah aktif di **Settings → For Developers**.
{: .prompt-info }

## Penutup

Kalau kamu masih sering buka CMD atau PowerShell klasik satu per satu, pindah ke Windows Terminal itu salah satu perubahan kecil yang langsung kerasa efeknya. Nggak perlu langsung ngoprek semua tema atau shortcut-nya — mulai aja dari pakai tab dan profil shell harianmu, sisanya bisa disesuaikan pelan-pelan sambil jalan.

![Oh My Posh terintegrasi dengan Windows Terminal](power-shell-cstm.png)
*Contoh tampilan Windows Terminal setelah dipasangkan dengan Oh My Posh.*

> Kalau nanti terminalnya udah nyaman dipakai dan pengen tampilan prompt yang lebih informatif (misal nampilin branch Git aktif), kamu bisa coba pasang [Oh My Posh](https://ohmyposh.dev/).
{: .prompt-tip }

> **Seri Panduan Windows & WSL:**
> 1. **Bagian 1: Mengenal Windows Terminal** *(kamu di sini)*
> 2. [Bagian 2: Mengenal WSL di Windows](/posts/wsl-di-windows/)
> 3. [Bagian 3: Setelah Install WSL, Apa Selanjutnya?](/posts/setelah-install-wsl-apa-selanjutnya/)
{: .prompt-info }
