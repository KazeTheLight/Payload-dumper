# 📦 Payload Dumper CI

Ekstrak partisi dari `payload.bin` OTA Android secara otomatis via GitHub Actions, tanpa perlu install apapun di PC.

Didukung oleh [payload-dumper-go](https://github.com/ssut/payload-dumper-go).

---

## ✨ Fitur

- ✅ Download OTA dari **Gofile**, **Pixeldrain**, atau URL langsung
- ✅ Nama file sesuai file asli yang didownload
- ✅ Ekstrak semua partisi atau partisi tertentu saja
- ✅ Hasil tersimpan sebagai **GitHub Actions Artifact**
- ✅ Opsional upload langsung ke **GitHub Release**

---

## 🚀 Cara Pakai

1. Buka tab **Actions**
2. Pilih workflow **Extract payload.bin**
3. Klik **Run workflow**
4. Isi form:

| Input | Keterangan | Contoh |
|-------|-----------|--------|
| `ota_url` | Link download OTA ZIP | `https://gofile.io/d/XXXXXX` |
| `partitions` | Partisi yang diekstrak (kosong = semua) | `boot,vendor_boot,init_boot` |
| `release_tag` | Tag release untuk upload (opsional) | `poco-f6-miui-dump` |

5. Tunggu workflow selesai (~5–15 menit tergantung ukuran OTA)
6. Download hasil di section **Artifacts** (tersimpan 7 hari)

---

## 🌐 Sumber yang Didukung

| Platform | Format URL |
|----------|-----------|
| Gofile | `https://gofile.io/d/XXXXXX` |
| Pixeldrain | `https://pixeldrain.com/u/XXXXXXXX` |
| Direct link | URL apapun yang langsung download file |

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

- Ukuran OTA besar (>3GB) mungkin memerlukan waktu lebih lama
- Artifact otomatis terhapus setelah **7 hari**
- GitHub Actions gratis tersedia **2.000 menit/bulan** untuk akun free

---

## 📄 Lisensi

MIT
