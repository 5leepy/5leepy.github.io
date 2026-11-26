# Writing Style Guide & Template Prompt Artikel

Panduan gaya bahasa untuk menjaga seluruh tulisan di blog ini tetap konsisten: santai, lugas, jujur, membumi, dan enak dibaca panjang.

---

## Prinsip Utama

1. **Pindahkan Karakter, Bukan Singkatan Chat Mentah**
   Jaga nada ngobrol yang santai, jujur, membumi, dan tidak menggurui agar artikel tetap nyaman dibaca panjang.
2. **Praktis & Realistis**
   Selipkan pengalaman nyata, batasan, *trade-off*, dan kendala di lapangan; hindari bahasa korporat, *hype*, atau klise AI.
3. **Ritme Terukur**
   Variasikan panjang kalimat dan jeda paragraf; singkatan kasual (*nggak, aja, buat, biar, pas, udah*) dipakai seperlunya saja untuk memberi napas obrolan, bukan di setiap kata.

---

## Sudut Pandang & Kebiasaan Blog Ini

* **Sudut pandang:** Gunakan **"saya"** untuk pengalaman penulis dan **"kamu"** untuk menyapa pembaca. Hindari gaya buku teks/diktat yang terlalu formal atau menggurui.
* **Istilah teknis:** Pakai istilah teknis/kerja secara alami (`WSL2`, `Docker`, `hardlink`, `Static Route`, `SLAAC`, dsb.) tanpa perlu dijelaskan kaku, kecuali memang relevan untuk pembaca baru.
* **Yang perlu dihindari (klise AI & nada brosur):**
  * Pola berulang *"bukan sekadar X, melainkan Y"*
  * Kata/frasa *hype*: *"membawa angin/udara segar"*, *"powerful"*, *"mendapatkan yang terbaik dari keduanya"*, *"tulang punggung"*, *"memang punya seni tersendiri"*
  * Paragraf terlalu padat yang menyambung 2–3 klausa panjang dengan terlalu banyak em-dash (`—`)
  * Penutup bergaya *copywriting* promosi atau janji artikel lanjutan yang belum pasti

---

## Template Prompt Artikel

Salin template ini saat menyusun draf artikel baru:

```text
Tuliskan artikel dengan gaya bahasa dan sudut pandang saya.

Karakter tulisan saya:
- Santai, lugas, jujur, membumi, dan tidak menggurui.
- Hindari bahasa kaku, formal berlebihan, kata-kata klise AI, atau klaim promosi yang lebay.
- Gunakan istilah teknis/kerja secara alami tanpa perlu dijelaskan secara kaku kecuali memang perlu.
- Selipkan nuansa praktis dari pengalaman nyata: akui batasan, trade-off, atau hal-hal yang sering bikin kendala di praktik.
- Gunakan variasi panjang kalimat dan jeda paragraf yang nyaman dibaca; singkatan kasual hanya dipakai sesekali untuk memberi nuansa obrolan yang wajar, bukan di setiap kata.
- Gunakan sudut pandang "saya" dan sapaan "kamu".

Topik / bahan artikel: [TEMPEL POIN-POIN / CATATAN / PENGALAMAN DI SINI]

Target pembaca & panjang artikel: [MISAL: pembaca umum/praktisi, sekitar 500-800 kata]
```

---

## Checklist Cepat Sebelum Publish

- [ ] Pembuka langsung masuk ke konteks masalah/pengalaman nyata (tanpa basa-basi generik).
- [ ] Minimal ada satu catatan **batasan, *trade-off*, atau kendala lapangan** yang jujur.
- [ ] Tidak ada frasa klise AI atau klaim berlebihan di judul, isi, maupun penutup.
- [ ] Ritme kalimat bervariasi (campuran pendek–sedang) dan paragraf tidak terlalu panjang.
- [ ] Frontmatter Jekyll (`title`, `description`, `date`, `categories`, `tags`, `image`) valid dan semua path gambar/link internal benar.
