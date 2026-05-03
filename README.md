# Undangan Pernikahan — Pink Floral Watercolor (Lipat 2 / Half-Fold)

Undangan cetak A5 lipat 2 (terlipat menjadi A6) dengan tema **pink floral watercolor**. Murni HTML + CSS + inline SVG — tidak butuh server, tidak butuh image eksternal.

---

## Struktur File

```
undangan/
├── index.html         ← Buka file ini di browser
├── assets/
│   └── style.css      ← Palette warna, font, layout, print rules
└── README.md
```

---

## Cara Pakai

### 1. Lihat preview di browser

- **Cara cepat:** double-click `index.html`
- **Via XAMPP:** buka `http://localhost/undangan/`

Akan tampil 2 sheet (Outer & Inner), masing-masing berukuran A5 landscape dengan 2 panel berdampingan dipisahkan garis lipat putus-putus.

### 2. Edit teks & detail

Buka `index.html` dengan editor (Notepad, VS Code, dsb) dan ubah bagian-bagian ini:

| Yang Diubah | Lokasi (cari teks ini) | Contoh |
|---|---|---|
| Nama panggilan di cover | `Syaiful <span class="amp">&amp;</span> Sarah` | `Sari & Bayu` |
| Tanggal di cover | `12 . 06 . 2026` | `28 . 09 . 2026` |
| Nama lengkap mempelai wanita | `Siti Sarah` | nama lengkap asli |
| Orang tua mempelai wanita | `Bpk. Hendra Wijaya` & `Ibu Lestari Kusuma` | nama asli |
| Nama lengkap mempelai pria | `Muhammad Nur Syaifullah` | nama lengkap asli |
| Orang tua mempelai pria | `Bpk. Bambang Setiawan` & `Ibu Sri Handayani` | nama asli |
| Hari & tanggal akad/resepsi | `Sabtu, 12 Juni 2026` | tanggal asli |
| Jam akad / resepsi | `09.00 WIB`, `11.00 — 14.00 WIB` | jam asli |
| Nama venue | `Aula Kenanga Ballroom` | nama gedung asli |
| Alamat lengkap | `Jl. Melati Indah No. 18,...` | alamat asli |
| Monogram di back panel | `S &amp; S` | inisial pasangan |
| Daftar Turut Mengundang | `<ul class="invitee-list">` (dua kolom) | tambah/hapus `<li>...</li>` sesuai keluarga |
| Kotak "Kepada Yth." (Cover) | `<div class="recipient-line"></div>` — kosong, untuk ditulis tangan saat distribusi | biarkan kosong, atau ketik nama untuk versi non-handwriting |

> **Tips:** posisi mempelai di "Inside-Left" bisa ditukar (pria di atas) — tinggal swap kedua blok `<div class="person">…</div>`.

### 2a. Ganti URL Google Maps di QR Code

Cari di `index.html` (panel Inside-Right) baris ini:

```html
<img class="qr-code"
     src="https://api.qrserver.com/v1/create-qr-code/?data=https%3A%2F%2Fmaps.app.goo.gl%2FSAMPLE&size=300x300&color=6B4F4F&bgcolor=FAF3F0&qzone=2&format=svg"
     alt="QR Code Google Maps Lokasi">
```

**Cara mengubah link Google Maps**:

1. Buka Google Maps → cari lokasi venue → klik **Share** → **Copy link** (mis. `https://maps.app.goo.gl/aBcDeFg123`).
2. **Encode URL** tersebut (ganti karakter spesial):
   - `https://` → `https%3A%2F%2F`
   - `/` → `%2F`
   - `?` → `%3F`, `&` → `%26`, `=` → `%3D`
   - **Cara cepat**: paste link di [urlencoder.org](https://www.urlencoder.org/) → copy hasil.
3. Ganti bagian `https%3A%2F%2Fmaps.app.goo.gl%2FSAMPLE` dengan hasil encode tadi.
4. Refresh browser → QR baru otomatis muncul.

> **Tidak ada internet saat preview/print?** Buka link QR di browser (paste URL `src` ke address bar) → klik kanan gambar → **Save image as** → simpan ke `assets/qr.svg`. Lalu ubah `src="..."` menjadi `src="assets/qr.svg"`. Setelah ini QR fully offline.

> **Custom warna QR**: ubah parameter `color=6B4F4F` (warna foreground, hex tanpa #) dan `bgcolor=FAF3F0` (background) di URL.

### 2b. Sketsa denah lokasi (SVG hand-drawn)

Di atas QR Code ada **sketsa denah lokasi** ukuran 80×26mm berupa inline SVG bergaya hand-drawn. Tidak butuh internet, fully offline, render perfect saat print.

**Element yang ada di sketsa default:**
- Jl. Raya Bogor (jalan utama horizontal) dengan arah ke Jakarta ↔ Cibinong
- Tol Cijago Exit (kotak pink kiri) — patokan eksit tol terdekat
- Pasar Cisalak (ikon kotak hijau tengah) — landmark referensi
- Jl. Cisalak Raya (cabang ke utara)
- Bintang pink ★ di posisi venue dengan label "Basecamp Konsep / venue"
- Compass U (utara) di pojok kanan atas

**Cara edit label/landmark**: buka `index.html`, cari `<!-- Sketsa denah lokasi (SVG hand-drawn style) -->` lalu ubah teks di dalam tag `<text>` masing-masing. Contoh:

```html
<text x="35" y="108" ...>Jl. Raya Bogor</text>          ← ubah jadi "Jl. Margonda"
<text x="155" y="60" ...>Pasar Cisalak</text>            ← ubah landmark
<text x="280" y="60" ...>Basecamp Konsep</text>          ← ubah nama venue
<text x="60" y="60" ...>Cijago Exit</text>               ← ubah eksit tol
```

**Cara geser posisi marker** (kalau bintang venue ingin pindah):
- Cari `<g transform="translate(280, 35)">` di SVG — ini blok bintang venue.
- Ubah `280` (x position) dan `35` (y position). ViewBox: 0–400 (lebar), 0–130 (tinggi).
- Geser ke kiri → kurangi x (mis. 250). Geser ke bawah → tambah y (mis. 50).

**Tambah landmark baru** (mis. "Mall Cijantung"):
- Copy salah satu blok existing (`<g transform="translate(...)">` + ikon + `<text>`)
- Paste di SVG, ubah koordinat dan label
- Save & refresh browser

> **Sketsa terlalu sederhana?** Kasih saya nama landmark/jalan area sekitar venue (mis. tol exit, mall, sekolah, masjid besar yang mudah dikenali) — saya tambahkan ke sketsa supaya lebih informatif buat tamu yang baru pertama datang.

### 3. Cetak ke PDF (rekomendasi pertama)

1. Buka `index.html` di **Chrome / Edge** (paling akurat untuk print CSS).
2. Tekan `Ctrl + P` (Windows) atau `Cmd + P` (Mac).
3. Atur opsi cetak:
   - **Destination:** Save as PDF
   - **Paper size:** A5
   - **Layout:** Landscape
   - **Margins:** Default *(atau None — keduanya OK)*
   - **Scale:** 100% / Default
   - **More settings → Background graphics:** ✅ **ON** *(WAJIB, supaya warna pink ikut tercetak)*
4. Klik **Save** → simpan sebagai `undangan-aria-rio.pdf`.

PDF yang dihasilkan = 2 halaman A5 landscape, bisa dibawa ke percetakan / di-print di rumah.

### 4. Cetak fisik 2 sisi

- Print **PDF di atas** ke kertas A5 dengan opsi **double-sided** (duplex).
- Setting flipping: **Flip on long edge** (bukan short edge).
- Lipat kertas **vertikal di tengah** (mengikuti garis lipat saat dibuka di browser).
- Hasil: booklet A6 dengan **Cover** di depan, **Greeting + Event** saat dibuka, **Quote + Monogram** di belakang.

> **Tidak punya printer A5?** Print di **A4 dengan opsi "Fit to page"** lalu potong di sekitar 210 × 148 mm. Atau bawa PDF ke percetakan digital — mereka biasa menerima A5.

### 5. Screenshot preview (untuk dibagikan WhatsApp dll.)

1. Buka `index.html` di browser, set zoom 100%.
2. Screenshot tiap sheet (gunakan `Win + Shift + S` di Windows, atau Snipping Tool).
3. Simpan sebagai `preview-cover.png`, `preview-inside.png`, `preview-back.png`.

---

## Kustomisasi Lanjutan

### Ganti warna pink ke shade lain
Buka `assets/style.css`, ubah variabel di `:root`:
```css
--blush:     #F8E1E7;   /* background utama */
--rose-soft: #E8B4BC;   /* sekunder */
--rose-deep: #C97B84;   /* aksen kuat (nama, judul) */
--gold:      #C9A66B;   /* aksen kecil (separator) */
```

### Tambah bleed 3mm untuk percetakan profesional
Ubah di `style.css`:
```css
@page { size: 216mm 154mm; margin: 0; }   /* A5 landscape + 3mm bleed */
.sheet { width: 216mm; height: 154mm; }
.panel { width: 108mm; height: 154mm; padding: 14mm 13mm; }
```
Lalu beri tahu percetakan: file sudah include 3mm bleed, trim ke 210 × 148 mm.

### Ganti ayat / kutipan
Cari `<p class="quote">` di `index.html` dan ganti isinya. Bisa pakai HTML `<br>` untuk pemisah baris.

### Versi non-Muslim
Hapus baris `<p class="bismillah">…</p>`, ganti `Insyā Allāh akan dilaksanakan` → `akan dilaksanakan`, ganti ayat di back-panel dengan quote pernikahan favorit.

---

## Catatan Teknis

- **Font:** Google Fonts (Cormorant Garamond, Great Vibes, Inter). Butuh internet saat **pertama** membuka — setelah itu di-cache browser. Jika offline saat print, font fallback ke serif/cursive lokal (masih rapi).
- **Ornamen:** semua bunga & daun adalah inline SVG yang digenerate via CSS dan `<symbol>` — bisa di-resize tanpa pecah.
- **Kompatibilitas:** Chrome, Edge, Firefox modern. Hindari Internet Explorer.
- **Tidak ada JavaScript** — pure HTML+CSS+SVG.

---

Selamat berbahagia atas pernikahannya 💗
