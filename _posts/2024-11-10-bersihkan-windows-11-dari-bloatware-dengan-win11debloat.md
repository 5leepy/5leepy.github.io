---
title: Bersihkan Windows 11 dari Bloatware dengan Win11Debloat
date: 2024-11-10
categories: [Tips & Trik, Windows]
tags: [windows11, debloat, win11debloat, powershell, optimasi]
---

Selamat datang di dunia Windows 11 yang serba baru! Tapi, di balik tampilannya yang modern dan fitur-fitur canggihnya, Windows 11 juga bawa "beban" yang nggak sedikit, yaitu *bloatware*. Aplikasi-aplikasi bawaan yang nggak penting ini cuma makan tempat di penyimpanan dan bikin laptop jadi lemot. 

Untungnya, ada cara mudah buat ngilangin *bloatware* ini, yaitu pake **Win11Debloat**! Win11Debloat adalah script PowerShell yang dibuat khusus buat *debloating* Windows 11 (dan Windows 10). Dengan Win11Debloat, kamu bisa hapus aplikasi-aplikasi bawaan yang nggak kamu butuhin, nonaktifin telemetri (pengiriman data ke Microsoft), dan optimasiin Windows 11 kamu agar lebih enteng dan ngebut.

Di postingan ini, aku bakal jelasin semua yang perlu kamu tahu tentang Win11Debloat, mulai dari cara pake, fitur-fiturnya, sampai tips dan peringatan penting. Siap-siap bersihin Windows 11 kamu dari *bloatware* ya!


## Apa Itu Bloatware?

Bloatware itu aplikasi yang udah terinstal di perangkat (laptop, HP, dll) sejak awal, tapi sebenernya nggak kita butuhin. Bayangin aja, kamu beli laptop baru, eh udah penuh aja sama aplikasi yang nggak jelas fungsinya. Itulah bloatware! 

Di Windows 11, ada banyak banget bloatware yang cuma makan tempat dan bikin laptop jadi lemot. Contohnya:

* Aplikasi-aplikasi bawaan yang jarang dipake: Kayak 3D Viewer, Get Help, Maps, dll.
* Game-game bawaan yang nggak seru: Siapa sih yang masih main Solitaire atau Minesweeper di tahun 2024? 
* Aplikasi-aplikasi dari pihak ketiga yang "nebeng" instalasi: Kayak antivirus McAfee, Spotify, atau aplikasi lain yang sebenarnya nggak kamu butuhin.

Nah, bloatware ini nggak cuma bikin laptop lemot, tapi juga bisa:

* **Makan tempat penyimpanan:** Bayangin aja kalau setiap aplikasi ukurannya ratusan MB, berapa GB yang kebuang cuma buat nyimpen bloatware?
* **Memperlambat proses booting:** Semakin banyak aplikasi yang jalan di startup, semakin lama laptop kamu nyala.
* **Mengganggu privasi:** Beberapa bloatware bisa ngirim data kamu ke developer tanpa sepengetahuan kamu.

Makanya, penting banget buat ngilangin bloatware dari Windows 11 kamu. Dan cara termudah buat nglakuinnya ya pake Win11Debloat!


## Kenapa Harus Pakai Win11Debloat?

Kamu mungkin bertanya-tanya, "Kenapa harus repot-repot pakai Win11Debloat? Emang nggak bisa hapus bloatware secara manual?"

Jawabannya, bisa aja sih. Tapi, coba bayangin:

* Kamu harus cari satu per satu aplikasi yang mau dihapus.
* Kamu harus hati-hati jangan sampai kehapus aplikasi yang penting.
* Prosesnya lama dan ribet. 

Nah, dengan Win11Debloat, semua itu jadi lebih mudah! Win11Debloat itu kayak "tukang bersih-bersih" khusus buat Windows 11 kamu. Dia bakal ngebersihin semua *bloatware* yang nggak penting, nonaktifin fitur-fitur yang ganggu, dan optimasiin Windows kamu biar lebih enteng dan ngebut.

## Cara Pakai Win11Debloat

Win11Debloat  bisa  dijalankan  dengan  dua  cara:  melalui  perintah  PowerShell  langsung  atau  dengan  men-download  script-nya.

>Pastikan kamu sudah backup data penting sebelum menjalankan Win11Debloat, ya! Meskipun Win11Debloat aman, tapi tetep aja ada baiknya kamu backup data penting dulu sebelum pake.
{: .prompt-warning }

### Menggunakan Perintah PowerShell


Buat kamu yang suka ngetik perintah dan pengen cara yang lebih "keren", bisa langsung pake PowerShell nih buat jalanin Win11Debloat.

>Selain menggunakan perintah PowerShell, kamu juga bisa men-download script Win11Debloat dan menjalankannya secara manual. Kamu bisa menemukan panduan lengkapnya di  [link ini](https://github.com/Raphire/Win11Debloat).
{: .prompt-info }

#### **Buka PowerShell sebagai administrator**

Pertama-tama, kamu perlu buka PowerShell dengan hak administrator. Caranya gampang:

1. Klik Start, ketik "PowerShell" 
2. klik kanan dan pilih "Run as administrator"

![Menjalankan PowerShell dari Start Menu](https://5leepy-img.netlify.app/win11debloat/startpowershell.png)

#### **Jalankan perintah PowerShell**

Setelah PowerShell terbuka, copy dan paste perintah berikut ke PowerShell:

```powershell
& ([scriptblock]::Create((irm "https://win11debloat.raphi.re/")))
```
{: .nolineno }

![Script Printah win11debloat](https://5leepy-img.netlify.app/win11debloat/psscript.png)

#### **Pilih mode dan ikuti petunjuk**

Tekan `Enter` dan tunggu sampai proses selesai. Nanti bakal muncul pilihan mode.

![Menu win11debloat](https://5leepy-img.netlify.app/win11debloat/win11debloat.png)

Win11Debloat punya dua mode utama:

* **Default:** Mode standar yang aman untuk pemula. Mode ini akan:
    * Menghapus bloatware seperti Get Help, Maps, Microsoft To Do, Skype, dll.
    * Menonaktifkan telemetri, diagnostic data, riwayat aktivitas, pelacakan aplikasi, dan iklan bertarget.
    * Menonaktifkan tips, trik, saran, dan iklan di Start Menu, Settings, notifikasi, dan File Explorer.
    * Menonaktifkan dan menghapus pencarian web Bing dan Cortana dari pencarian Windows.
    * Menonaktifkan Windows Copilot.
    * Menampilkan ekstensi file untuk tipe file yang dikenal.
    * Menonaktifkan layanan widget dan menyembunyikan ikonnya dari taskbar.

* **Custom:** Mode untuk mengatur sendiri aplikasi dan fitur yang ingin dihapus.

>Pilih mode yang sesuai dengan kebutuhanmu. Jika ragu, pilih mode Default saja.
{: .prompt-tip }

## Parameters

Win11Debloat mendukung berbagai parameter yang bisa kamu gunakan untuk menyesuaikan proses debloating. Berikut beberapa contoh parameter yang bisa kamu gunakan:

### Contoh penggunaan parameter:

```powershell
& ([scriptblock]::Create((irm "https://win11debloat.raphi.re/"))) -RunDefaults -Silent
```
{: .nolineno }

* `-Silent`: Menekan semua prompt interaktif, sehingga script akan berjalan tanpa memerlukan input pengguna.
* `-Sysprep`: Menjalankan script dalam mode Sysprep. Semua perubahan akan diterapkan ke profil pengguna default Windows dan hanya akan memengaruhi akun pengguna baru.
* `-RunDefaults`: Menjalankan script dengan pengaturan default.
* `-RemoveApps`: Menghapus pilihan default aplikasi bloatware.
* `-RemoveAppsCustom`: Menghapus semua aplikasi yang ditentukan dalam file 'CustomAppsList'.
* `-DisableBing`: Menonaktifkan dan menghapus pencarian web Bing, Bing AI & Cortana di pencarian Windows.
* `-DisableTelemetry`: Menonaktifkan telemetri, data diagnostik & iklan bertarget.
* `-RevertContextMenu`: Mengembalikan menu konteks gaya Windows 10 yang lama. (Hanya Windows 11)
* `-TaskbarAlignLeft`: Menyelaraskan ikon taskbar ke kiri. (Hanya Windows 11)
* `-DisableCopilot`: Menonaktifkan dan menghapus Windows Copilot. (Hanya Windows 11)

>Jika kamu ingin mengembalikan perubahan yang dilakukan oleh Win11Debloat, kamu bisa mengikuti panduan di [link ini](https://github.com/Raphire/Win11Debloat/discussions/114).
{: .prompt-tip }

## Penjelasan Perintah:

Buat yang penasaran, nih aku jelasin sedikit tentang perintah PowerShell yang kita pake:

```powershell
& ([scriptblock]::Create((irm "https://win11debloat.raphi.re/")))
```
{: .nolineno }

Perintah ini  memang  terlihat  agak  ribet  ya,  tapi  sebenarnya  fungsinya  simpel  kok.  Intinya,  perintah  ini  bakal  download  dan  jalanin  script  Win11Debloat  langsung  dari  internet.  Gimana  caranya?  Nih  aku  jelasin  bagian  per  bagian:

* `irm "https://win11debloat.raphi.re/"` :
    * `irm` adalah singkatan dari `Invoke-RestMethod`. Fungsinya untuk mendownload konten dari URL yang diberikan.
    * `"https://win11debloat.raphi.re/"` adalah URL yang menyimpan script Win11Debloat.
    * Jadi, bagian ini berfungsi untuk mendownload script Win11Debloat dari internet.

* `([scriptblock]::Create(...))` :
    * Bagian ini berfungsi untuk membuat "script block" dari konten yang sudah di-download tadi. Script block adalah sebuah unit kode PowerShell yang bisa dieksekusi.
* `& (...)` :
    * Tanda `&` di PowerShell digunakan untuk menjalankan perintah atau script.
    * Jadi, bagian ini berfungsi untuk menjalankan script block yang sudah dibuat tadi.

Dengan  menggabungkan  ketiga  bagian  tersebut,  perintah  PowerShell  ini  akan  mendownload  script  Win11Debloat  dari  internet  dan  menjalankannya  secara  otomatis.  Praktis kan?

___

Gimana? Udah siap ngilangin bloatware dari Windows 11 kamu? Cobain Win11Debloat deh, dijamin laptop atau PC kamu bakal lebih enteng dan ngebut!