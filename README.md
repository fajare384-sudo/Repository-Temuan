# Simulasi Temuan Reviu — Bantuan Pangan 2026 | BPK RI

## 🚀 Deploy ke GitHub Pages (Tanpa GitHub Actions)

### Langkah 1 — Buat Repository

1. Login [github.com](https://github.com) → klik **"New"**
2. Nama repo bebas, misal: `simulasi-banpang` → pilih **Public** → **Create repository**

### Langkah 2 — Upload File

Di halaman repo baru, klik **"uploading an existing file"**

Upload **4 file berikut** (drag & drop semua sekaligus):

```
index.html        ← Aplikasi utama
_config.yml       ← Konfigurasi Jekyll
.nojekyll         ← Nonaktifkan Jekyll (file kosong)
README.md         ← File ini
```

> **Windows — file `.nojekyll` tidak terlihat?**
> Buka File Explorer → tab **View** → centang **Hidden items**
> File `.nojekyll` akan muncul. Sertakan saat upload.

Klik **Commit changes**

### Langkah 3 — Aktifkan GitHub Pages

1. Klik tab **Settings** di repo
2. Klik **Pages** di sidebar kiri
3. **Source** → pilih **"Deploy from a branch"**
4. Branch: **`main`** | Folder: **`/ (root)`**
5. Klik **Save**

### Langkah 4 — Buka Aplikasi

Tunggu **1–2 menit**, lalu akses:

```
https://<username>.github.io/<nama-repo>/
```

Status build bisa dipantau di tab **Actions** (muncul otomatis).

---

## Jika Masih Error

| Gejala | Solusi |
|--------|--------|
| Halaman 404 | Tunggu 2–3 menit lagi, atau hard refresh (Ctrl+Shift+R) |
| Build gagal di Actions | Pastikan `_config.yml` ikut ter-upload |
| Halaman kosong/blank | Pastikan nama file persis `index.html` (huruf kecil) |
| `.nojekyll` tidak bisa diupload | Tidak masalah — `_config.yml` dan front matter di `index.html` sudah cukup |

---

## 📋 Fitur

- Upload XLSX/XLS/CSV data BAST (>500.000 baris)
- 22 aturan deteksi: BPK KHP + APIP CPP + Fisik/Kualitas
- Klaster SP4N-LAPOR, APIP CPP, Jenis Koreksi terintegrasi
- Rekapitulasi per Kabupaten / Kecamatan / Desa
- Tab Referensi APIP: matriks silang 3 kerangka
- Ekspor Excel/CSV langsung dari browser
- Mode Demo (KC Bulungan, Paser & Berau)
- **Data tidak dikirim ke server — semua berjalan lokal di browser**

---

⚠️ *Kandidat temuan awal — wajib diverifikasi manual sebelum dijadikan dasar LHP.*
