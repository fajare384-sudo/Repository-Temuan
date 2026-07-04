# Dasbor Audit Bantuan Pangan

Dasbor audit lapangan untuk temuan anomali data Bantuan Pangan (BULOG). Situs statis
satu halaman (`index.html`) — tidak perlu server backend, build step, atau database.
Semua pemrosesan data (upload `.xlsx`, filter, ekspor) berjalan di peramban pengguna.

## Isi berkas

- `index.html` — seluruh aplikasi (HTML/CSS/JS + data temuan yang sudah ter-embed).
- `.github/workflows/deploy.yml` — GitHub Actions untuk auto-deploy ke GitHub Pages
  setiap kali ada push ke branch `main`.

Dependensi eksternal (dimuat lewat CDN, butuh koneksi internet saat dipakai):
- [SheetJS/xlsx](https://cdnjs.com/libraries/xlsx) — baca/tulis berkas Excel.
- [Leaflet](https://leafletjs.com/) + [OpenStreetMap](https://www.openstreetmap.org/) — peta prioritas kunjungan lapangan.
- [Nominatim](https://nominatim.openstreetmap.org/) — geocoding nama kecamatan/kabupaten menjadi koordinat (dipanggil hanya saat tombol "Cari koordinat & tampilkan peta" diklik, hasilnya di-cache di `localStorage` browser).

Tidak ada proses build (npm/webpack/dsb) — repo ini bisa langsung disajikan sebagai situs statis.

## Cara deploy ke GitHub Pages

### Opsi A — otomatis lewat GitHub Actions (sudah disiapkan)

1. Buat repository baru di GitHub, lalu push seluruh isi folder ini ke branch `main`:

   ```bash
   git init
   git add .
   git commit -m "Initial commit: dasbor audit bantuan pangan"
   git branch -M main
   git remote add origin https://github.com/USERNAME/NAMA-REPO.git
   git push -u origin main
   ```

2. Di GitHub: **Settings → Pages → Build and deployment → Source**, pilih
   **GitHub Actions** (bukan "Deploy from a branch").
3. Workflow di `.github/workflows/deploy.yml` akan otomatis berjalan setiap push ke
   `main` dan mem-publish situsnya. Lihat progresnya di tab **Actions**.
4. Setelah selesai, situs bisa diakses di:
   `https://USERNAME.github.io/NAMA-REPO/`

### Opsi B — manual, tanpa Actions

1. Push isi folder ini ke branch `main` (boleh hapus folder `.github` kalau tidak
   ingin memakai Actions).
2. Di GitHub: **Settings → Pages → Build and deployment → Source**, pilih
   **Deploy from a branch**, pilih branch `main` dan folder `/ (root)`.
3. Simpan. Situs akan tersedia dalam beberapa menit di
   `https://USERNAME.github.io/NAMA-REPO/`.

## Menjalankan secara lokal

Karena ini cuma berkas statis, cukup buka `index.html` langsung di browser, atau
jalankan server statis sederhana supaya fitur upload/fetch berjalan mulus:

```bash
python3 -m http.server 8000
# lalu buka http://localhost:8000
```

## Catatan penggunaan

- **Unggah data baru**: tombol "Unggah" di kanan atas menerima berkas `.xlsx` dengan
  sheet bernama mengandung kata "Temuan" (idealnya "Temuan Anomali Data"). Data hasil
  unggahan digabung ke data yang sudah ada, sepenuhnya di sisi klien — tidak ada data
  yang terkirim ke server mana pun.
- **Peta prioritas kunjungan**: klik "Cari koordinat & tampilkan peta". Proses geocoding
  membatasi diri ±1 permintaan/detik ke Nominatim (sesuai kebijakan penggunaan mereka)
  dan menyimpan hasilnya di `localStorage`, jadi hanya perlu dicari sekali per lokasi.
- **Ekspor**: tombol "Ekspor hasil (.xlsx)" mengekspor baris yang lolos filter saat ini
  ke berkas Excel untuk rencana kunjungan lapangan.
- Karena `index.html` berukuran ~5 MB (data temuan ter-embed di dalamnya), pastikan
  Git tidak mengubahnya jadi LFS placeholder secara tidak sengaja — batas GitHub untuk
  berkas biasa adalah 100 MB, jadi ukuran ini masih jauh aman.

## Privasi data

Berkas `index.html` memuat data pribadi (nama, NIK, alamat) hasil audit. Sebelum
menjadikan repository ini **publik**, pastikan itu memang sudah sesuai kebijakan
instansi Anda — atau gunakan repository **private** (GitHub Pages tetap bisa dipakai
untuk repo private di akun/organisasi dengan paket GitHub Pro/Team/Enterprise, dengan
situs yang hanya bisa diakses oleh kolaborator repo tersebut).
