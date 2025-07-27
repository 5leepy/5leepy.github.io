---
title: Mengenal Windows Terminal — Masa Depan CLI di Windows
description: Windows Terminal adalah terminal modern yang menggantikan CMD dan PowerShell klasik. Pelajari fitur-fitur utamanya dan kenapa ini wajib dicoba oleh pengguna Windows.
date: 2025-07-24 22:00:00 +0700
comments: true
categories: [Tips & Trik,Windows]
tags: [windows, terminal, cli, powershell, wsl, productivity]
media_subpath: /windows-guide/win-terminal/
image:
  path: terminal-thumbnail.webp
  lqip: data:image/webp;base64,UklGRrQAAABXRUJQVlA4IKgAAAAwBgCdASoyABsAP6HC2V86Mq0lLBqsy0A0CWwAvvxOVhw/o+TLbKZB7IW04KGPnGq5S6YqTNgs8Oj+AP68ckjgsjgnwSCsOgfPASiqixN8/Xt86VGtWI6ax    +bFjdG0tbRYeplPLq7p3FPHAZT1dG0ROcweM20PMP1wLZSs0JXwYAyJ1Otnr46vdK5RtI7gPS86/Vc1q0Z6ZagqYGoaHPwuJM3bnB4fgAA=
  alt: "Mulai kenal Windows Terminal: satu aplikasi untuk PowerShell, CMD, WSL, dan lebih banyak lagi."
---

Windows Terminal adalah aplikasi terminal modern yang dirancang untuk menggantikan PowerShell klasik dan Command Prompt. Microsoft pertama kali memperkenalkannya pada tahun 2019 sebagai bagian dari upaya memperbarui pengalaman baris perintah di Windows.

Terminal ini bukan sekadar pembungkus visual, melainkan sebuah emulator terminal yang powerful. Ia memungkinkan kita menjalankan berbagai shell seperti PowerShell, Command Prompt, WSL (Windows Subsystem for Linux), Git Bash, hingga SSH, semuanya dari satu jendela terpusat yang modern dan dapat dikustomisasi.

![Tampilan Windows Terminal dengan beberapa tab aktif](windows-terminal-tabs.png)
*Windows Terminal memungkinkan banyak shell dibuka dalam satu jendela tab*

## Mengapa Terminal?

Sebelum membahas Windows Terminal, mari kita mundur sedikit dan bertanya: “Mengapa kita menggunakan terminal?”

Terminal memungkinkan kita:

* Mengotomatisasi pekerjaan dengan script
* Mengeksekusi perintah dengan cepat tanpa klik berulang
* Mengakses dan mengontrol sistem lebih dalam
* Menjalankan tool berbasis teks, seperti git, curl, atau ffmpeg

PowerShell sendiri adalah shell dan bahasa pemrograman powerful buatan Microsoft. Dengan PowerShell, kita bisa:

```powershell
Get-Process          # Melihat proses yang berjalan
Get-Service          # Melihat status service
Get-ChildItem        # Sama seperti ls/dir
Set-ExecutionPolicy  # Mengatur hak eksekusi script
```

> Banyak administrator sistem dan developer mengandalkan PowerShell untuk scripting dan automasi.
{: .prompt-info }

## Windows Terminal vs PowerShell dan CMD Klasik

Berikut beberapa kelebihan Windows Terminal dibanding CMD dan PowerShell klasik:

### 1. **Multiple Tabs**

Tidak perlu lagi membuka banyak jendela CMD. Terminal mendukung banyak tab seperti browser. Kita bisa membuka satu tab PowerShell, satu tab Ubuntu (WSL), dan satu lagi Command Prompt — semua dalam satu jendela.

> Gunakan `Ctrl+Shift+T` untuk membuka tab baru
{: .prompt-tip }

### 2. **Split Panes**

![Split panes horizontal dan vertikal di Windows Terminal](windows-terminal-split-panes.png)
*Split panes sangat berguna saat bekerja multitasking antar shell.*


Kita bisa membagi layar terminal menjadi beberapa panel secara horizontal atau vertikal, menjalankan perintah yang berbeda di tiap panel.

> Shortcut default untuk split horizontal: `Alt+Shift+-`, vertical: `Alt+Shift++`
{: .prompt-tip }

### 3. **Profiles untuk Semua Shell**

![Menu profiles di Windows Terminal](windows-terminal-profiles.png)
*Profiles bisa dikustom untuk tiap shell, lengkap dengan ikon dan nama.*

Terminal ini bisa jadi pusat dari semua CLI tool kita. Misalnya:

* PowerShell
* CMD
* Git Bash
* Ubuntu via WSL
* Azure CLI
* SSH

Masing-masing bisa kita atur dengan nama, warna, font, bahkan ikon sendiri.

### 4. **Customisasi Tampilan Total**

Windows Terminal mendukung:

* Tema gelap dan terang
* Font kustom seperti Cascadia Code
* Transparansi dan efek akrilik
* Skema warna personal

![Contoh pengaturan tampilan tema](windows-terminal-themes.png)
*Windows Terminal mendukung berbagai tema dan font modern.*

> Semua konfigurasi bisa diubah dari file `settings.json`
{: .prompt-info }

> Hati-hati saat mengedit `settings.json`, perubahan yang salah bisa menyebabkan crash saat terminal dijalankan.
{: .prompt-warning }

### 5. **Dukungan Unicode dan UTF-8**

Terminal ini mampu menampilkan karakter internasional dan simbol Unicode dengan lebih baik. Cocok untuk kamu yang bekerja dengan teks multi-bahasa atau karakter khusus seperti emoji, simbol matematika, atau bahasa non-Latin.

### 6. **Quake Mode dan Command Palette**

* **Quake Mode**: tekan `Win + ^` (default) untuk membuka terminal dari atas layar — mirip seperti terminal di game Quake.

![Quake Mode aktif di Windows Terminal](windows-terminal-quake.png)
*Tekan `Win + ^` untuk membuka terminal dengan gaya drop-down dari atas layar.*

* **Command Palette**: tekan `Ctrl+Shift+P` untuk mencari dan mengeksekusi command seperti di VSCode.

![Command Palette di Windows Terminal](windows-terminal-command.png)  
*Command Palette memudahkan akses cepat ke berbagai perintah tanpa harus mengetik secara manual.*

> Fokus mode juga tersedia untuk tampilan fullscreen minimalis
{: .prompt-info }

### 7. **Pengalaman Lebih Cepat dan Konsisten**

Windows Terminal menggunakan GPU rendering dengan DirectWrite/DirectX untuk hasil teks yang tajam dan halus.

> Jalankan sebagai administrator hanya saat diperlukan. Menjalankan script dengan hak admin tanpa verifikasi bisa berbahaya.
{: .prompt-danger }

## Instalasi Windows Terminal

Cara paling mudah:

![Halaman Windows Terminal di Microsoft Store](terminal-store.png)
*Windows Terminal dapat diunduh langsung dari Microsoft Store.*

1. Buka **Microsoft Store**
2. Cari “Windows Terminal”
3. Klik **Install**

> Disarankan menggunakan versi dari Microsoft Store karena akan mendapatkan update otomatis
{: .prompt-tip }

Atau via command line:

### Menggunakan `winget`

```powershell
winget install --id Microsoft.WindowsTerminal -e
```

### Menggunakan PowerShell (untuk Windows 10/11)

```powershell
Invoke-WebRequest -Uri https://aka.ms/terminal -OutFile Terminal.msixbundle
Add-AppxPackage .\Terminal.msixbundle
```

> Pastikan Anda sudah mengaktifkan sideloading apps di Settings → For Developers
{: .prompt-info }

## Penutup

Windows Terminal membawa udara segar ke dunia terminal di Windows. Fitur seperti multiple tab, split pane, profiles, dan kustomisasi membuatnya lebih dari sekadar pembungkus PowerShell. Ia adalah pusat kendali baru untuk semua aktivitas command-line Anda.

Jadi, jika kamu masih menggunakan PowerShell klasik atau CMD biasa, saatnya mencoba sesuatu yang lebih segar, fleksibel, dan menyenangkan.

![Oh My Posh terintegrasi dengan Windows Terminal](power-shell-cstm.png)
*Oh My Posh mempercantik prompt terminal dengan gaya powerline dan icon modern.*

> Ingin mencoba sesuatu yang lebih keren? Coba gabungkan Windows Terminal dengan \[Oh My Posh] untuk prompt terminal yang elegan.
{: .prompt-tip }
