---
title: "Dari WSL ke Home Lab Docker dan Era AI: Catatan Kecil 2026"
description: Cerita santai soal perjalanan dari ngoprek Windows Terminal dan WSL di 2025, lanjut bikin home lab Docker di laptop bekas, sampai berubahnya cara ngoding bareng AI agent di 2026.
date: 2026-11-18 17:00:00 +0700
comments: true
categories: [AI & Workflow]
tags: [homelab, docker, antigravity, workflow, logbook]
---

Kalau kamu sempat mampir ke arsip blog ini, tulisan terakhir saya tayang pertengahan 2025 — waktu itu masih rajin bahas soal **Windows Terminal** dan **WSL**. Setelah itu blog ini sempat vakum cukup lama. Bukan karena bosen ngoprek sih, tapi memang aktivitas di belakang layar lagi banyak berubah.

Anggap aja tulisan ini semacam *update* santai buat nyambungin cerita dari 2025 ke 2026.

## Awalnya Cuma WSL, Eh Lanjut ke Laptop Bekas

Kebiasaan main di terminal Linux lewat WSL ternyata nular ke mana-mana. Perintah-perintah dasar kayak pindah folder, ngatur *permission* file, sampai SSH yang awalnya cuma buat iseng nyoba di Windows, lama-lama jadi makanan sehari-hari.

Dari situ kepikiran: daripada cuma muter-muterin *container* di laptop kerja, kenapa nggak sekalian manfaatin laptop bekas nganggur di rumah buat jadi server kecil yang nyala terus?

Jadilah **home lab** rumahan saya. Nggak pakai server *rack* mahal — cukup satu laptop lama yang hemat listrik, install Docker, terus atur semua *stack*-nya pakai **Dockge** biar gampang dipantau lewat web. Sekarang di atasnya udah jalan **Pi-hole** buat ngeblokir iklan dan *tracker* satu rumah, plus paket lengkap **\*arr stack** (Sonarr, Radarr, Prowlarr, Bazarr, Jellyseerr) bareng **qBittorrent** buat otomasi tontonan keluarga.

Cerita detail arsitekturnya — termasuk pelajaran soal *unified volume mount* biar *hardlink* bisa jalan instan — sudah saya rangkum di halaman [Homelab](/homelab/).

## Cara Kerja yang Berubah: Ngobrol dan Ngerancang Bareng AI Agent

Tapi kalau ditanya apa yang paling berubah di 2026, jawabannya bukan hardware-nya, melainkan **cara saya ngerjain dan ngerawat proyek**.

Dulu, mau ngoding sesuatu atau sekadar ngerapihin blog aja rasanya berat di waktu. Harus duduk lama di depan editor, ngetik baris demi baris kode atau *config* secara manual. Di tengah kesibukan kerja dan ngurus tiga anak di rumah, sering banget ide ngoprek akhirnya cuma jadi wacana karena keburu kehabisan waktu.

Sekarang polanya jauh beda berkat **AI-assisted building** bareng agent seperti **Antigravity**. Tugas saya nggak lagi ngetik semuanya dari nol sendirian, tapi lebih ke nentuin arah, desain, batasan teknis, dan ngecek hasil akhirnya.

*Refresh* blog ini sendiri contoh nyatanya:
* Semua gambar yang dulu masih numpang di CDN luar sekarang sudah dipindahin ke lokal di `assets/img/` biar blog lebih mandiri dan aman.
* Konfigurasi tema Chirpy dibersihin, termasuk matiin *cache* PWA yang dulu sering bikin tampilan baru telat muncul di browser.
* Halaman [About](/about/) dan tab [Homelab](/homelab/) juga ikutan diperbarui biar nyambung sama apa yang beneran saya kerjain sekarang.

## Lanjut ke Depan

Blog ini tetap saya pakai sesuai niat awalnya: jadi *logbook* pribadi yang jujur, santai, dan praktis. Ke depannya saya pengen nulis hal-hal yang beneran kepake dan jalan di meja kerja maupun jaringan rumah saya sendiri — mulai dari urusan WSL, catatan ngoprek *home lab* Docker, sampai eksperimen *workflow* bareng AI agent.

Sampai ketemu di catatan ngoprek berikutnya!
