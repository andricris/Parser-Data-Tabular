# Data Tabular v2

Aplikasi web statis untuk mengonversi data matriks dari Excel menjadi tabel data terstruktur (cabang, kode produk, nama produk, quantity, HPP) dengan pencarian/filter per kolom. Cocok untuk kebutuhan rekapitulasi stok/penjualan sederhana tanpa server backend.

## Fitur Utama

- **Konversi data matriks ke tabel baris** (baris per kombinasi cabang & produk).
- **Auto-fill Nama Produk & HPP** dari `database.json`.
- **Filter per kolom** (Cabang, Kode Produk, Nama Produk, Quantity, HPP).
- **Opsi sembunyikan Qty 0** agar tabel lebih ringkas.
- **Salin hasil** ke clipboard lengkap dengan header.
- **Tampilan modern** dengan Bootstrap 5 + font Poppins.

## Prasyarat

- Browser modern (Chrome, Edge, Firefox, Safari).
- Tidak memerlukan server khusus; cukup buka file HTML.

## Cara Menjalankan

1. Buka file `index.html` dengan browser (double-click atau drag & drop ke browser).
2. Pastikan file `database.json` berada di folder yang sama dengan `index.html`.

> Jika Anda menjalankan melalui server lokal (opsional), Anda bisa memakai:
>
> ```bash
> python -m http.server 8000
> ```
>
> Lalu buka `http://localhost:8000`.

## Cara Menggunakan

1. Salin data dari Excel dalam bentuk matriks.
2. Tempel di kolom **Data Input**.
3. Klik **Proses Data** untuk konversi.
4. (Opsional) Centang **Sembunyikan Qty 0** agar baris dengan quantity 0 disembunyikan.
5. Gunakan kolom filter untuk menyaring data.
6. Klik **Salin Hasil** untuk menyalin tabel ke clipboard.

### Format Input yang Didukung

- **Baris pertama**: header berisi nama cabang di kolom pertama, lalu **kode produk** di kolom berikutnya.
- **Baris berikutnya**: data cabang pada kolom pertama, lalu **quantity** per kode produk.

Contoh:

```
Cabang   P37JYPL1  P9216180
bks1     1         10
tgr1     0         4
```

Hasilnya akan menjadi baris seperti:

| Cabang | Kode Produk | Nama Produk | Quantity | HPP |
|--------|-------------|------------|----------|-----|
| bks1   | P37JYPL1     | ...        | 1        | ... |
| bks1   | P9216180     | ...        | 10       | ... |
| tgr1   | P37JYPL1     | ...        | 0        | ... |
| tgr1   | P9216180     | ...        | 4        | ... |

## Struktur Data `database.json`

`database.json` berisi array objek dengan kunci berikut:

```json
[
  {
    "Part No": "P37JYPL1",
    "Part Description": "Nama produk",
    "hpp": 51963
  }
]
```

### Cara Memperbarui Database

1. Edit file `database.json` (tambah/ubah item produk).
2. Buka `index.html` dan perbarui nilai `lastUpdateDate` agar badge menampilkan tanggal update terbaru.

Contoh:

```js
const lastUpdateDate = "09/10/2025"; // Format: DD/MM/YYYY
```

## Struktur Project

```
.
├── index.html     # Aplikasi utama
├── test.html      # Salinan halaman untuk kebutuhan uji (opsional)
└── database.json  # Data master produk
```

## Catatan

- **Quantity tidak boleh mengandung titik (.)** karena input di-parse sebagai integer.
- Jika kode produk tidak ditemukan di database, kolom **Nama Produk** akan berisi `--- TIDAK DITEMUKAN ---` dan HPP akan 0.

## Lisensi

Belum ada informasi lisensi pada repository ini. Silakan tambahkan bila diperlukan.
