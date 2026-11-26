---

title: "Mengenal WSL: Jalankan Linux di Windows Tanpa Dual Boot"
description: "Cara menjalankan Linux langsung di Windows pakai WSL tanpa ribet dual boot. Bahas bedanya WSL 1 vs WSL 2, cara install, sampai catatan trade-off di pemakaian harian."
date: 2025-07-27 01:00:00 +0700
comments: true
categories: [Windows & WSL]
tags: [wsl, linux, terminal, windows, cli, productivity, developer]
media_subpath: /assets/img/posts/windows-guide/wsl-intro/
image:
  path: wsl-thumbnail.webp
  lqip: data:image/webp;base64,UklGRvAAAABXRUJQVlA4IOQAAAAUBACdASp4AEEAEDj+AAASvwnzKL7+w8K/8nf/OSnQOtZX7ZFtewoOAAD+4tUtqppzGx7MiAdNW+J7Wp54lqcJFHmxEtmDzLkBSV45KLJXk+lJwaQ6w8W79ght9aRleparqtfDv6OGjEKkw9VXfe3dWLVR8G3Rrs3v3uWcMMUeRLhrrv7CfYGX9U0QvM+Nq/uRFOZG9lkamC7xLxGJ6oih5dREKq0UEdUyBhu86d1TolwNY+JD03LLfTjKPV5yILbnlkTqLj8ijFSKRnjvmFPne0XvrG6VlVp+6um23YIBAAAAAAA=
  alt: "WSL memungkinkan menjalankan Linux langsung di Windows tanpa dual boot."
---

Dulu, kalau mau nyoba Linux dari laptop Windows, opsinya cuma dua: dual boot atau pasang VirtualBox/VMware. Dual boot bikin bolak-balik restart setiap kali butuh aplikasi Windows, sedangkan VM tradisional sering bikin kipas laptop langsung ngebut karena makan resource besar.

Sekarang ada jalan tengah yang jauh lebih praktis: **WSL (Windows Subsystem for Linux)**. Kamu bisa jalanin shell Ubuntu atau Debian langsung di samping aplikasi Windows, tanpa reboot dan tanpa ribet ngatur tampilan VM.

> Lewat WSL, perintah Linux, manajemen paket `apt`, sampai environment backend dan Docker bisa langsung jalan dari Windows.
{: .prompt-info }

## Apa Itu WSL?

Singkatnya, WSL adalah fitur resmi Windows untuk menjalankan lingkungan Linux langsung di dalam sistem operasi Windows. Pertama kali muncul di Windows 10, dan sekarang sudah masuk versi 2 (WSL 2).

Bedanya dengan VirtualBox yang biasa kita kenal, WSL 2 jalan di atas VM ringan berbasis Hyper-V yang terintegrasi rapat dengan Windows. Startup-nya cuma hitungan detik, jendela terminalnya nyatu dengan Windows Terminal, dan kamu nggak perlu repot atur partisi disk atau resolusi layar desktop Linux.

---

## WSL 1 vs WSL 2 — Apa Bedanya?

| Fitur                 | WSL 1                          | WSL 2                            |
| --------------------- | ------------------------------ | -------------------------------- |
| Arsitektur            | Translasi syscall              | Kernel Linux asli via Hyper-V    |
| Kecepatan file I/O    | Lebih cepat akses file Windows | Lebih cepat untuk file Linux     |
| Kompatibilitas Docker | ❌ Tidak didukung               | ✅ Didukung penuh                 |
| Pemakaian resource    | Lebih ringan                   | Lebih besar, tapi jauh lebih kompatibel |

> Untuk pemakaian sekarang, langsung pakai **WSL 2** aja — apalagi kalau nanti mau jalanin Docker, PostgreSQL, Nginx, atau ngoding backend.
{: .prompt-tip }

---

## Cara Install WSL di Windows

### 🔁 Cara Cepat (Windows 10/11 versi terbaru)

Buka PowerShell atau Windows Terminal sebagai Administrator, lalu jalankan:

```powershell
wsl --install
```

Satu perintah ini langsung mengaktifkan fitur WSL, mengunduh kernel Linux, dan memasang distro default (biasanya Ubuntu). Setelah restart, tinggal bikin username dan password Linux, lalu langsung siap dipakai.

### 🛠️ Cara Manual (kalau cara cepat gagal)

Di beberapa versi Windows 10 lama atau kondisi jaringan tertentu, `wsl --install` kadang gagal. Kalau kejadian, bisa pakai jalur manual:

1. Aktifkan fitur WSL dan platform virtualisasi:

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

2. Unduh dan install kernel WSL 2 dari: [https://aka.ms/wsl2kernel](https://aka.ms/wsl2kernel)

3. Set default ke WSL 2:

```powershell
wsl --set-default-version 2
```

4. Buka **Microsoft Store**, cari distro seperti "Ubuntu", lalu klik **Install**.

![Tampilan Microsoft Store untuk Ubuntu](ubuntu-mstore.png)
*Ubuntu di Microsoft Store — cukup klik Install lalu tunggu proses inisialisasi awal.*

> Versi dari Microsoft Store umumnya paling gampang dirawat karena update paket aplikasinya ikut otomatis.
{: .prompt-info }

---

## Distro Linux Apa Saja yang Bisa Dipakai?

Beberapa distro yang paling sering dipakai di WSL:

* **Ubuntu** — pilihan paling aman buat mulai, dokumentasi dan jawabannya di internet paling banyak.
* **Debian** — ringan dan stabil, saya pribadi juga suka pakai ini buat keperluan server atau container.
* **Kali Linux** — kalau fokusmu di keamanan jaringan atau pentest.
* **Arch Linux** — buat yang memang suka ngoprek dari nol.

> Kamu bisa pasang lebih dari satu distro sekaligus dan membukanya lewat `wsl -d <nama_distro>`.
{: .prompt-tip }

---

## Akses File Windows & Linux

WSL punya jembatan akses file dua arah:

* Dari Linux ke Windows: lewat `/mnt/c/Users/NamaUser/`
* Dari Windows ke Linux: lewat `\\wsl$\\Ubuntu\\home\\username`

Satu hal penting yang sering bikin pengguna baru kaget: akses file Windows dari dalam WSL 2 (`/mnt/c/...`) itu **jauh lebih lambat** kalau isinya ribuan file kecil seperti folder `node_modules` atau repo `git`. Jadi buat urusan ngoding, biasakan taruh proyek di direktori Linux (`/home/username`).

> Simpan source code di direktori Linux (`/home/username`) supaya `git`, `npm`, atau proses build nggak terasa lemot.
{: .prompt-info }

---

## Kenapa WSL Enak Dipakai Kerja & Ngoding?

Buat saya yang sehari-hari masih butuh Windows tapi workflow-nya banyak ketemu Linux, WSL itu nolong banget karena:

* Tool CLI seperti `git`, `npm`, `python`, `curl`, sampai `ssh` jalan natural di habitat aslinya
* Bisa jadi backend buat Docker tanpa perlu mesin Linux terpisah
* Terintegrasi langsung dengan **Windows Terminal** dan **VS Code**
* Enak dipakai nyimulasikan environment server Linux lokal sebelum deploy

---

## Integrasi WSL dengan VS Code

Kalau pakai VS Code, cukup pasang ekstensi **WSL** (dulu namanya Remote - WSL). Setelah itu, dari folder proyek di terminal Linux, tinggal ketik:

```bash
code .
```

VS Code di Windows bakal langsung kebuka, tapi terminal dan prosesnya jalan di dalam Linux.

> Jalankan `code .` langsung dari direktori Linux (`/home/...`), bukan dari `/mnt/c/...`, biar kerasa ngebutnya.
{: .prompt-tip }

---

## Catatan Praktis & Trade-off

Supaya ekspektasinya realistis, WSL 2 bukan tanpa kekurangan. Ada dua hal yang biasanya cepat terasa kalau sudah dipakai rutin:

1. **RAM (`vmmemWSL`) bisa lumayan rakus:** Secara default, WSL 2 boleh mengambil sampai separuh RAM laptop buat cache Linux dan nggak selalu langsung dibalikin ke Windows. Solusinya, batasi jatah RAM lewat file `.wslconfig`:

```powershell
wsl --shutdown
notepad "$env:USERPROFILE/.wslconfig"
```

2. **Bukan pengganti 100% Linux bare-metal:** Untuk kasus yang butuh akses hardware langsung (misal passthrough USB tertentu atau GPU Linux murni), kadang tetap ada batasan dibanding install Linux langsung. Tapi untuk 90% kebutuhan dev, scripting, dan belajar server, WSL 2 udah lebih dari cukup.

Selain itu, gabungkan WSL dengan **Windows Terminal** (dan **Quake Mode** lewat `` Win + ` `` di layout keyboard US) supaya pindah-pindah tab antara Windows dan Linux nggak ribet.

---

## Penutup

WSL itu jalan tengah yang paling masuk akal kalau kamu butuh ekosistem Linux tapi belum mau — atau belum bisa — meninggalkan Windows. Setup awalnya nggak sampai sepuluh menit, dan kalau suatu saat nggak cocok, tinggal dihapus tanpa utak-atik partisi disk.

![Contoh penggunaan WSL di Windows Terminal](wsl-terminal.png)
*Debian via WSL yang dibuka di Windows Terminal.*

Kalau WSL-nya sudah terpasang tapi masih bingung harus mulai ngapain di dalam terminal Linux, lanjut ke bagian berikutnya di bawah ini.

> **Seri Panduan Windows & WSL:**
> 1. [Bagian 1: Mengenal Windows Terminal](/posts/windows-terminal-cli/)
> 2. **Bagian 2: Mengenal WSL di Windows** *(kamu di sini)*
> 3. [Bagian 3: Setelah Install WSL, Apa Selanjutnya?](/posts/setelah-install-wsl-apa-selanjutnya/)
{: .prompt-info }
