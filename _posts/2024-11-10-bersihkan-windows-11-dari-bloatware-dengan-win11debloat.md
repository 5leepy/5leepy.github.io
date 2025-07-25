---
title: Bersihkan Windows 11 dari Bloatware dengan Win11Debloat
description: Windows 11 terasa lambat karena bloatware? Pelajari tentang Win11Debloat, script PowerShell ampuh untuk membersihkan aplikasi bawaan, menonaktifkan telemetri, dan optimasi performa.
author: nadir
date: 2024-11-10 00:34:00 +0700
comments: true
categories: [Tips & Trik, Windows]
tags: [windows11, debloat, win11debloat, powershell, optimasi]
media_subpath: /windows-guide/win11debloat/
image:
  path: flying-script.webp
  lqip: data:image/webp;base64,UklGRhYBAABXRUJQVlA4IAoBAAD0AwCdASpwAFIAADj+AAASnOuAk//2P/Vmaa7CdKk43B0aClPn4tFAAP7l39eyAHzzkdLu+rTmsqZn+syFMGaJ0KdcamTunGWLjbM9/Y9X/dUUTK19fDCTSrGHcD8j0ijSkd1q1WoHg0ycVrI9l/zlgFAuNUNXx41jtzgpXU4yzS6EkAwIq82JGIsplLfeuzV7wKUia4iFHeJRRLsF5nWQsNt4tBqNss4b9g6nGok9IraZzAmjZ4gvLpl1bNiVbYoM1Y8B8nUhTEVf7FjnKGCVvlku9vKdtIXkeJ3tKzmIX3QSQP9vvaz3OW/UJK9sQ/CNLS3POq/NpjA42uoreRhhq4GU883RMAAAAA==
  alt: Representasi visual kode program atau data yang sedang dioptimasi.
---

# Win11Debloat: Bersihkan Windows 11 dari Bloatware

Windows 11 memang tampil modern dan penuh fitur baru. Tapi sayangnya, banyak juga aplikasi bawaan yang nggak penting alias *bloatware*. Aplikasi ini makan ruang, bikin performa melambat, dan bahkan bisa ganggu privasi. Solusinya? Pakai **Win11Debloat** — script PowerShell simpel tapi ampuh buat bersihin Windows 11 kamu dari hal-hal yang nggak dibutuhin.

## Apa Itu Bloatware?

*Bloatware* adalah aplikasi bawaan yang jarang (atau bahkan nggak pernah) dipakai. Misalnya:

* 3D Viewer, Get Help, Maps
* Game klasik kayak Solitaire atau Candy Crush
* Aplikasi pihak ketiga seperti McAfee atau Spotify

Selain bikin penuh storage, bloatware juga:

* Memperlambat startup
* Ganggu privasi dengan kirim data tanpa sepengetahuan
* Menambah beban sistem secara keseluruhan

## Kenapa Harus Pakai Win11Debloat?

Win11Debloat menyederhanakan proses menghapus bloatware dan mengoptimalkan Windows. Daripada hapus satu-satu secara manual, tool ini langsung jalanin skrip otomatis yang aman dan bisa dikustom.

### Fitur Utama:

* Menghapus aplikasi bawaan yang tidak penting
* Menonaktifkan telemetri dan pelacakan
* Menyembunyikan iklan dan tips yang mengganggu
* Menonaktifkan Copilot, Widgets, dan Bing Search
* Bisa dijalankan dalam mode Default (aman) atau Custom (lebih fleksibel)

## Cara Menjalankan Win11Debloat

### 1. Buka PowerShell sebagai Administrator

* Klik Start > ketik “PowerShell” > klik kanan > **Run as administrator**

![Buka PowerShell](startpowershell.png)

### 2. Jalankan Perintah Berikut

```powershell
& ([scriptblock]::Create((irm "https://win11debloat.raphi.re/")))
```

![Menjalankan Script](psscript.png)

### 3. Pilih Mode: Default atau Custom

![Opsi Mode](win11debloat.png)

* **Default Mode** (rekomendasi): Aman dan cukup untuk sebagian besar pengguna
* **Custom Mode**: Buat kamu yang mau pilih sendiri aplikasi/fitur mana aja yang dihapus

> 💡 **Tips**: Selalu backup data penting sebelum menjalankan script.
{: .prompt-tip }

## Contoh Penggunaan Parameter

Mau otomatis tanpa prompt? Gunakan opsi parameter:

```powershell
& ([scriptblock]::Create((irm "https://win11debloat.raphi.re/"))) -RunDefaults -Silent
```

### Parameter yang Tersedia:

* `-Silent`: Jalankan tanpa prompt interaktif
* `-Sysprep`: Terapkan ke akun pengguna baru
* `-RunDefaults`: Mode default otomatis
* `-DisableBing`, `-DisableTelemetry`, `-DisableCopilot`, dll

> 🔁 Untuk rollback (mengembalikan perubahan), cek panduan resmi di [GitHub](https://github.com/Raphire/Win11Debloat/discussions/114).
{: .prompt-info }

## Kesimpulan

Kalau kamu merasa Windows 11 kamu terlalu berat dan penuh aplikasi nggak penting, Win11Debloat adalah solusi cepat dan aman. Cuma butuh PowerShell dan satu baris perintah buat bersihin semua bloatware dan bikin sistem kamu lebih ringan, cepat, dan privat.

> 🧹 **Waktunya bersih-bersih Windows 11 kamu!**

Kunjungi [repo resminya di GitHub](https://github.com/Raphire/Win11Debloat) buat info lebih lengkap dan update terbaru.
