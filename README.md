# Nadir Nahdi — Dokumentasi, Proyek, dan Eksperimen

[![Build and Deploy](https://github.com/5leepy/5leepy.github.io/actions/workflows/pages-deploy.yml/badge.svg)](https://github.com/5leepy/5leepy.github.io/actions/workflows/pages-deploy.yml)
[![Website](https://img.shields.io/website?url=https%3A%2F%2F5leepy.github.io&label=5leepy.github.io)](https://5leepy.github.io)

Repositori kode sumber untuk blog teknologi pribadi milik Nadir Nahdi, dapat diakses secara langsung di **[https://5leepy.github.io](https://5leepy.github.io)**.

Blog ini berfungsi sebagai catatan publik dan *logbook* teknis berisi dokumentasi, panduan praktis, catatan proyek, serta hasil eksperimen seputar sistem dan pengembangan perangkat lunak.

## Topik Utama

- **Windows & WSL** — Konfigurasi Windows Terminal, alur kerja *command-line*, dan pengembangan di Windows Subsystem for Linux.
- **Home Lab & Docker** — Eksplorasi *self-hosting*, kontainerisasi, dan pengelolaan layanan di lingkungan *home lab*.
- **Linux** — Catatan penggunaan, konfigurasi, dan utilitas sistem Linux.
- **Frontend & Eksperimen** — Eksperimen pengembangan web, antarmuka pengguna, serta proyek kecil lainnya.

## Tech Stack

- **Static Site Generator:** Jekyll 4.4
- **Theme:** [Chirpy Theme](https://github.com/cotes2020/jekyll-theme-chirpy) 7.6
- **Hosting & CI/CD:** GitHub Pages + GitHub Actions ([`pages-deploy.yml`](.github/workflows/pages-deploy.yml))
- **Komentar:** [Giscus](https://giscus.app/) (berbasis GitHub Discussions)

## Struktur Singkat

```text
.
├── .github/workflows/   # Workflow CI/CD untuk build dan deploy ke GitHub Pages
├── _posts/              # Artikel dan catatan blog dalam format Markdown
├── _tabs/               # Halaman navigasi utama (About, Archives, Categories, Tags)
├── _config.yml          # Konfigurasi utama situs Jekyll dan tema Chirpy
├── Gemfile              # Daftar dependensi Ruby/Jekyll
└── tools/               # Skrip bantu untuk menjalankan dan menguji situs secara lokal
```

## Cara Menjalankan Lokal

Pastikan **Ruby** dan **Bundler** sudah terpasang di sistem Anda, lalu jalankan perintah berikut:

1. **Clone repositori ini:**

   ```bash
   git clone https://github.com/5leepy/5leepy.github.io.git
   cd 5leepy.github.io
   ```

2. **Install dependensi:**

   ```bash
   bundle install
   ```

3. **Jalankan server pengembangan lokal:**

   ```bash
   bundle exec jekyll s
   ```

   Atau gunakan skrip bantu yang sudah tersedia (mendukung *live reload*):

   ```bash
   ./tools/run.sh
   ```

   Setelah berjalan, buka `http://127.0.0.1:4000` di peramban Anda.

## Lisensi

Proyek ini dilisensikan di bawah lisensi MIT. Lihat berkas [LICENSE](LICENSE) untuk informasi selengkapnya.
