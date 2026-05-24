# 📦 Payload Dumper & Firmware Dumper CI

Ekstrak partisi dari firmware Android secara otomatis via GitHub Actions, tanpa perlu install apapun di PC.

Mendukung format **OTA ZIP** (dengan `payload.bin`) maupun **Fastboot ROM** (`.img` langsung).
Didukung oleh [payload-dumper-go](https://github.com/ssut/payload-dumper-go).

---

## ✨ Fitur

- ✅ Auto-deteksi format ZIP (OTA payload vs Fastboot ROM)
- ✅ Download dari berbagai platform hosting
- ✅ Nama file sesuai file asli yang didownload
- ✅ Ekstrak semua partisi atau partisi tertentu saja
- ✅ Hasil tersimpan sebagai **GitHub Actions Artifact**
- ✅ Opsional upload langsung ke **GitHub Release**

---

## 🌐 Platform yang Didukung

| Platform | Format URL |
|----------|-----------|
| Gofile | `https://gofile.io/d/XXXXXX` |
| Pixeldrain | `https://pixeldrain.com/u/XXXXXXXX` |
| MediaFire | `https://www.mediafire.com/file/...` |
| Google Drive | `https://drive.google.com/file/d/...` |
| OneDrive | `https://1drv.ms/...` atau `https://onedrive.live.com/...` |
| SourceForge | `https://sourceforge.net/projects/.../files/...` |
| AndroidFileHost | `https://androidfilehost.com/?fid=...` |
| Direct Link | URL apapun yang langsung download file |

---

## 🚀 Cara Pakai

1. Buka tab **Actions**
2. Pilih workflow **Extract Firmware**
3. Klik **Run workflow**
4. Isi form:

| Input | Keterangan | Contoh |
|-------|-----------|--------|
| `ota_url` | Link download firmware/OTA | `https://gofile.io/d/XXXXXX` |
| `partitions` | Partisi yang diekstrak (kosong = semua) | `boot,vendor_boot,init_boot` |
| `release_tag` | Tag release untuk upload (opsional) | `poco-f6-a15-dump` |

5. Tunggu workflow selesai (~5–15 menit tergantung ukuran file)
6. Download hasil di section **Artifacts** (tersimpan 7 hari)

---

## 🔍 Auto-Deteksi Format

Workflow otomatis mendeteksi isi ZIP:

| Kondisi | Mode | Aksi |
|---------|------|------|
| Ada `payload.bin` di dalam ZIP | OTA | Ekstrak → dump via payload-dumper-go |
| Ada `.img` langsung di dalam ZIP | Fastboot ROM | Ekstrak `.img` langsung ke output |
| Tidak ada keduanya | — | Error + tampilkan isi ZIP |

---

## 📂 Output

Setiap partisi diekstrak sebagai file `.img` terpisah, contoh:

```
boot.img
vendor_boot.img
init_boot.img
system.img
vendor.img
product.img
odm.img
...
```

Semua file juga dikompres menjadi `extracted_partitions.zip`.

---

## ⚙️ Konfigurasi Lanjutan

### Ekstrak partisi tertentu saja
Isi field `partitions` dengan nama partisi dipisah koma:
```
boot,vendor_boot,init_boot
```

### Upload ke GitHub Release
Isi field `release_tag` dengan nama tag:
```
device-codename-android-version
```
File `.img` dan ZIP akan otomatis ter-attach ke release tersebut.

---

## ⚠️ Catatan

- OTA berukuran besar (>3GB) memerlukan waktu lebih lama
- Artifact otomatis terhapus setelah **7 hari**
- GitHub Actions gratis tersedia **2.000 menit/bulan** untuk akun free
- Google Drive: file yang dibatasi/private tidak bisa didownload
- OneDrive: hanya mendukung link sharing publik

---

## 📄 Lisensi

MIT
