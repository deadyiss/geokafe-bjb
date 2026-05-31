# ☕ GeoKafe BJB


**Direktori & Peta Interaktif Cafe — Banjarbaru & Martapura**

WebGIS berbasis satu file HTML yang menampilkan persebaran cafe di wilayah Kota Banjarbaru dan Kabupaten Banjar (Martapura), dilengkapi filter, analitik, dan deteksi status buka/tutup secara real-time.

---
## Akses Github Pages
URL : https://deadyiss.github.io/geokafe-bjb/

## Scrernshots
### Loading Screen
<img width="1303" height="692" alt="image" src="https://github.com/user-attachments/assets/f0db4b4a-cbad-44f6-8d3a-b2e55b20d0f5" />

### Tampilan Utama
<img width="1839" height="832" alt="image" src="https://github.com/user-attachments/assets/f64051ee-2d62-45a5-8213-4a1f23c0e860" />

### Dashboard Analitik
<img width="1839" height="555" alt="image" src="https://github.com/user-attachments/assets/6754d7f1-acbe-4bf6-8d43-a65b403fbb64" />

### Card Cafe
<img width="934" height="500" alt="image" src="https://github.com/user-attachments/assets/da528e46-ce81-488d-921b-6daeadd44963" />




---
## Fitur

- **Peta Interaktif** — marker berwarna per kategori cafe, cluster otomatis saat zoom out
- **Cluster Tooltip** — hover pada cluster menampilkan rincian jumlah cafe per kategori di dalamnya
- **Search Ganda** — cari berdasarkan nama cafe atau nama kecamatan secara bersamaan
- **Quick Filter Kecamatan** — chip klik cepat untuk 8 kecamatan di Banjarbaru dan Martapura
- **Filter Kategori & Harga** — pill toggle untuk Kopi / Non-Kopi / Keduanya dan Budget / Mid / Premium
- **Filter Rating** — slider minimum rating 1.0–5.0
- **Status Buka/Tutup** — deteksi otomatis berdasarkan jam browser vs. jam operasional, ditampilkan sebagai dot pada marker dan badge pada panel detail
- **Panel Detail** — klik marker untuk membuka card detail di sisi kanan peta (nama, kecamatan, alamat, jam buka, rating)
- **Heatmap** — toggle visualisasi kepadatan sebaran cafe
- **Dashboard Analitik** — 3 chart (bar kategori, donut distribusi harga, bar horizontal top 5 rating), collapsible
- **Upload CSV** — ganti data sample dengan data sendiri
- **Sidebar Toggle** — sidebar bisa disembunyikan untuk memaksimalkan area peta

---

## Cara Pakai

Tidak perlu instalasi, server, atau build tool.

1. Download file `index.html`
2. Buka langsung di browser (Chrome / Firefox / Edge)
3. Koneksi internet diperlukan untuk memuat tile peta dan library CDN

> Tile peta menggunakan **CartoDB Positron**, bukan OpenStreetMap default, sehingga tidak mengalami error `403 Access Blocked` saat dibuka dari `file://` lokal.

---

## Stack Teknologi

| Library | Versi | Fungsi |
|---|---|---|
| [Leaflet.js](https://leafletjs.com) | 1.9.4 | Rendering peta interaktif |
| [Leaflet.markercluster](https://github.com/Leaflet/Leaflet.markercluster) | 1.5.3 | Clustering marker |
| [Leaflet.heat](https://github.com/Leaflet/Leaflet.heat) | latest | Layer heatmap |
| [Chart.js](https://www.chartjs.org) | 4.4.0 | Dashboard analitik |
| [PapaParse](https://www.papaparse.com) | 5.4.1 | Parsing file CSV upload |
| [Tailwind CSS](https://tailwindcss.com) | CDN | Utility styling |
| CartoDB Positron | — | Tile basemap (tanpa API key) |

Semua library dimuat via CDN. Tidak ada `npm install`, tidak ada build process.

---

## Struktur Data

### Data Sample (Hardcoded)

Data sample sudah tertanam di dalam file HTML sebagai JavaScript array `SAMPLE_DATA`, berisi 18 cafe di 8 kecamatan.

### Upload CSV Kustom

Untuk mengganti data sample dengan data sendiri, siapkan file `.csv` dengan kolom berikut:

```
nama_cafe,kecamatan,latitude,longitude,alamat,kategori,jam_buka,kisaran_harga,rating
```

| Kolom | Tipe | Nilai yang Valid |
|---|---|---|
| `nama_cafe` | string | Nama cafe |
| `kecamatan` | string | Nama kecamatan |
| `latitude` | number | Koordinat lintang (desimal) |
| `longitude` | number | Koordinat bujur (desimal) |
| `alamat` | string | Alamat lengkap |
| `kategori` | string | `Kopi` / `Non-Kopi` / `Keduanya` |
| `jam_buka` | string | Format `HH:MM – HH:MM` (contoh: `08:00 – 22:00`) |
| `kisaran_harga` | string | `Budget` / `Mid` / `Premium` |
| `rating` | number | Angka desimal `1.0` – `5.0` |

Baris dengan `latitude` atau `longitude` kosong/tidak valid akan dilewati otomatis.

#### Rentang Kisaran Harga

| Label | Rentang |
|---|---|
| Budget | < Rp 30.000 |
| Mid | Rp 30.000 – Rp 70.000 |
| Premium | > Rp 70.000 |

---

## Kecamatan yang Dicakup

**Kota Banjarbaru**
- Banjarbaru Utara
- Banjarbaru Selatan
- Cempaka
- Landasan Ulin
- Liang Anggang

**Kabupaten Banjar (Martapura)**
- Martapura Kota
- Martapura Barat
- Martapura Timur

---

## Struktur File

```
index.html   ← satu-satunya file yang diperlukan
README.md
```

Seluruh HTML, CSS, dan JavaScript berada dalam satu file. Tidak ada dependensi eksternal selain koneksi internet untuk CDN.

---

## Warna Marker

| Kategori | Warna |
|---|---|
| Kopi | Biru (#6366F1) |
| Non-Kopi | Oranye (#F97316) |
| Keduanya | Hijau (#10B981) |

Dot kecil di pojok kanan atas marker menunjukkan status saat ini:

| Warna dot | Status |
|---|---|
| Hijau | Buka sekarang |
| Merah | Tutup |

Status dihitung otomatis dengan membandingkan jam browser terhadap kolom `jam_buka`. Format `HH:MM – HH:MM` dengan midnight crossing (contoh: `22:00 – 02:00`) didukung.

---

## Catatan Pengembangan

- Deteksi buka/tutup bergantung pada jam lokal browser pengguna dan akurasi data `jam_buka` di CSV
- Data sample bersifat simulasi untuk keperluan demonstrasi — koordinat dan nama cafe bukan data resmi
- Untuk deployment di web server publik, tidak ada konfigurasi tambahan yang diperlukan selain mengunggah file HTML

---

## Lisensi

Proyek ini dibuat untuk keperluan tugas kuliah. Library yang digunakan masing-masing memiliki lisensi tersendiri (Leaflet: BSD 2-Clause, Chart.js: MIT, PapaParse: MIT).
