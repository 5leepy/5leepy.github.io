---
title: "Dari WSL ke Home Lab Docker dan Era AI: Catatan Kecil 2026"
description: Refleksi perjalanan dari belajar Windows Terminal dan WSL di 2025 hingga menjalankan home lab Docker di laptop bekas serta membangun proyek bersama AI agent di 2026.
date: 2026-11-18 17:00:00 +0700
comments: true
categories: [AI & Workflow]
tags: [homelab, docker, antigravity, workflow, logbook]
---

Kalau melihat arsip blog ini, tulisan terakhir saya terbit pada pertengahan 2025 — saat itu saya masih banyak menulis panduan dasar seputar **Windows Terminal** dan **WSL**. Setelah itu, blog ini sempat cukup lama sepi. Bukan karena berhenti bereksperimen, justru karena kesibukan di belakang layar sedang bergeser cukup drastis.

Tulisan ini adalah catatan kecil untuk menjembatani jeda waktu dari 2025 ke 2026.

## Berawal dari WSL, Berlanjut ke Laptop Bekas

Membiasakan diri dengan terminal Linux lewat WSL ternyata membawa efek domino yang menyenangkan. Perintah dasar seperti navigasi direktori, manajemen izin file, dan SSH yang dulu hanya dipakai untuk mencoba-coba di Windows, pelan-pelan berubah menjadi kebutuhan harian.

Langkah berikutnya terasa alami: daripada hanya menjalankan *container* di lingkungan lokal, kenapa tidak memanfaatkan laptop bekas di rumah sebagai server kecil yang menyala terus?

Dari sana lahirlah **home lab** rumahan saya. Tidak perlu perangkat *rack* mahal — cukup satu laptop lama yang hemat daya, dipasang Docker, lalu diatur rapi menggunakan **Dockge** sebagai manajer Docker Compose. Di atasnya kini berjalan **Pi-hole** untuk menyaring iklan dan *tracker* di seluruh jaringan rumah, serta ekosistem **\*arr stack** (Sonarr, Radarr, Prowlarr, Bazarr, Jellyseerr) bersama **qBittorrent** untuk otomasi media keluarga.

Detail arsitekturnya — termasuk pelajaran penting soal *unified volume mount* agar *hardlink* berjalan instan — sudah saya rangkum di halaman khusus [Homelab](/homelab/).

## Pergeseran Cara Kerja: Merancang Bersama AI Agent

Perubahan terbesar di 2026 justru bukan pada perangkat kerasnya, melainkan pada **cara saya membangun dan merawat proyek**.

Dulu, proses ngoding atau merapikan blog seperti ini menuntut banyak waktu di depan editor untuk menulis baris demi baris kode atau konfigurasi secara manual. Di tengah kesibukan kerja dan mengurus tiga anak di rumah, seringkali ide eksperimen berhenti di tengah jalan karena waktu eksekusinya tidak cukup.

Sekarang, alur kerja saya bergeser ke **AI-assisted building** bersama agent seperti **Antigravity**. Peran saya bukan lagi mengetik semuanya dari nol, melainkan menentukan arah, arsitektur, batasan desain, dan melakukan verifikasi hasil.

Pembaruan blog ini sendiri adalah contoh nyatanya:
* Seluruh aset gambar yang sebelumnya bergantung pada CDN eksternal kini dipindahkan secara lokal ke `assets/img/` agar blog sepenuhnya mandiri dan tahan banting.
* Konfigurasi tema Chirpy dibersihkan, termasuk menonaktifkan *cache* PWA yang sering membuat pembaruan tampilan terlambat muncul di browser.
* Halaman [About](/about/) dan tab [Homelab](/homelab/) diperbarui agar benar-benar mencerminkan apa yang sedang saya kerjakan saat ini.

## Melangkah ke Depan

Blog ini tetap setia pada tujuan awalnya: menjadi *logbook* pribadi yang jujur dan praktis. Topik ke depan tidak lagi terpatok pada teori yang belum sempat saya sentuh, melainkan langsung berangkat dari apa yang benar-benar berjalan di meja kerja dan jaringan rumah saya — mulai dari WSL, operasional *home lab* Docker, hingga eksperimen *workflow* bersama AI agent.

Sampai ketemu di catatan eksperimen berikutnya!
