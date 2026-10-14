# SINTESA – Portal Layanan Akademik FST Unpatti

**Tugas Pertemuan 5: Responsive & Accessible Web Client**
Nama: Maglensya Yulya Supusepa | NIM: 202451065

Satu halaman web client (HTML + CSS, tanpa JavaScript) untuk layanan akademik: Surat Aktif Kuliah, Transkrip Sementara, Cuti Akademik, dan Legalisir Dokumen.

- **URL aplikasi:** _isi link GitHub Pages / Netlify_
- **Repo GitHub:** _isi link repo_

## Struktur proyek

```
├── index.html
├── css/styles.css
├── img/logo.png
├── evidence/        (screenshot DevTools)
└── README.md
```

## Fitur sesuai ketentuan

| Ketentuan | Implementasi |
|---|---|
| Struktur semantik | `header`, `nav`, `main` (3 `section`), `article` per kartu, `footer`; heading h1 → h2 → h3 |
| Kartu layanan | 4 kartu, masing-masing punya heading dan link |
| Form | 6 field: nama, NIM, email, jenis layanan (select), cara pengambilan (radio dalam `fieldset`), keperluan (textarea); label terasosiasi; tombol `<button type="submit">` |
| Validasi HTML | `required`, `type="email"`, `pattern` NIM, `minlength`/`maxlength` |
| Responsive | Mobile-first; 1 kolom, 2 kolom (40em), 4 kolom (64em) |
| Tanpa overflow | Diuji di 360, 768, dan 1280 px |
| Keyboard | Skip link, urutan Tab logis, focus ring emas dengan tepi gelap |
| Gambar | Logo informatif, `alt="Logo Universitas Pattimura"`; tidak ada gambar dekoratif |
| CSS layout | Grid untuk kartu dan footer, Flexbox untuk header dan menu |

## Bukti pemeriksaan DevTools

| Pemeriksaan | Hasil | Bukti |
|---|---|---|
| Elements | Landmark `header`, `nav`, `main`, `footer` terbaca; box model diperiksa di Computed | `evidence/01-elements.png` |
| Responsive 360 px | Satu kolom, tanpa scroll horizontal | `evidence/02-360.png` |
| Responsive 768 px | Kartu 2 kolom, tanpa scroll horizontal | `evidence/03-768.png` |
| Responsive 1280 px | Kartu 4 kolom, tanpa scroll horizontal | `evidence/04-1280.png` |
| Network (awal) | `favicon.ico` berstatus 404 | `evidence/05-network.png` |
| Network (setelah perbaikan) | Semua resource berstatus 200 | `evidence/05b-network-setelah.png` |
| Accessibility tree | `<nav>` berperan `navigation`, nama "Navigasi utama" | `evidence/06-a11y-tree.png` |
| Lighthouse | Skor Accessibility 100 | `evidence/07-lighthouse.png` |
| Keyboard | Fokus terlihat jelas pada field form | `evidence/08-keyboard.png` |
| Validasi form (kosong) | Browser menolak kolom wajib yang kosong | `evidence/09-validasi.png` |
| Validasi form (email salah) | Browser menolak format email tidak valid | `evidence/09b-validasi-email.png` |

## Temuan debugging

| No | Temuan | Alat DevTools | Perbaikan |
|----|--------|---------------|-----------|
| 1 | `favicon.ico` berstatus 404 dan muncul lencana error merah di DevTools. | Network | Menambahkan `<link rel="icon" href="img/logo.png">` di `<head>`. Setelah reload tidak ada lagi resource gagal. |
| 2 | Menu "Kontak" turun ke baris kedua di lebar 360 px. | Responsive Mode | Tidak diperbaiki karena disengaja: `flex-wrap` mencegah overflow horizontal. |
| 3 | Kontras warna oranye awal berisiko di bawah 4.5:1. | Lighthouse | Warna utama digelapkan ke `#b34700` dan `#7a2f00`. Skor Accessibility menjadi 100. |
| 4 | Dropdown "Jenis layanan" sempat terisi otomatis sehingga `required` tidak berfungsi. | Uji form di browser | Menambahkan opsi kosong `<option value="">Pilih layanan</option>`. Kolom kosong kini ditolak. |

## Keputusan desain

- **Mobile-first:** satu kolom sebagai dasar, breakpoint ditambahkan saat konten mulai lega (40em dan 64em), bukan berdasarkan nama perangkat.
- **Semantic-first:** elemen native (`nav`, `label`, `fieldset`, `button`) dipakai sebelum ARIA. Satu-satunya ARIA adalah `aria-label` pada `nav` dan `aria-describedby` untuk petunjuk field.
- **Kontras dan fokus:** warna gelap untuk teks putih, focus ring dua lapis (emas dan gelap) agar terlihat di latar terang maupun gelap, target sentuh minimal 44 px.
- **Form tanpa JavaScript:** `action="#"` sehingga pengiriman hanya memuat ulang halaman, karena JavaScript tidak wajib pada tugas ini.