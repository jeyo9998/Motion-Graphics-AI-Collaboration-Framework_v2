# Fixture Inventory — `D:/Download/update` (2026-11-24)

Data ini dibaca langsung dari berkas yang owner sediakan. Pada hari yang sama owner meminta fixture dipindah ke repository: salinan kini tinggal di [`../fixtures/`](../fixtures/README.md) (hash cocok satu per satu), sedangkan **berkas asli di `D:/Download/update` tetap utuh** — yang dilakukan adalah salin, bukan pindah. Direktori ini mencatat sumber awal dan properti yang terbaca saat inspeksi pertama.

## Perintah reproduksi

```bash
cd "D:/Download/update"
sha256sum XML/*.xml aep/*.aep
head -c 420 XML/movement_1.xml                      # header pembuatan Alight Motion
for f in XML/*.xml; do printf '%s ' "$f"; grep -o '<kf ' "$f" | wc -l; done
tr -c '[:print:]' '\n' < aep/Motion_Graphics_Unik_Camera.aep | grep -a -E 'ADBE Camera|Camera 1' | head
tr -c '[:print:]' '\n' < aep/movement_1.aep | grep -a 'dc:format' | head -1
```

## Alight Motion — XML teks (3 berkas)

| Berkas | Ukuran | Judul `<scene>` | Kanvas | fps | `<kf>` | Elemen menonjol |
|---|---:|---|---|---:|---:|---|
| `XML/Motion_Graphics_unik.xml` | 276.954 B | `cr:kroni_asgrd` | 1440×1080 | 20 | 345 | 182 `shape`, 304 `transform`, 164 `effect`, 1011 `property` |
| `XML/movement_1.xml` | 3.115 B | `Proyek Baru 94` | 1920×1080 | 120 | 19 | 2 `shape` + 1 `nullobj`, 1 `rotation`, 2 `bookmark` |
| `XML/movement_2.xml` | 1.940 B | `Proyek Baru 95` | 1920×1080 | 120 | 8 | 1 `shape`, 2 `rotation`, 1 `size` |

SHA-256:

```
c31748fa2140a586446a77fd9091a6e508cabf777a6370d36ede3a928d879a32  XML/Motion_Graphics_unik.xml
8d7010a8e8bf9e156210b147ec4e63687290f03378443b8d86a74d6c1467f1dc  XML/movement_1.xml
6c8083f1a814039d410903386a433600826104a89120a108fd2c4bb4db2f4dda  XML/movement_2.xml
```

Tanda pengenal pada ketiga berkas (komentar header dan atribut `<scene>`):

```
Created by Alight Motion (http://alightmotion.com)
am="com.alightcreative.motion/5.0.273.1028425"   amver="1028425"
amplatform="android"   ffver="106"
```

Tanggal ekspor tercatat pada header: 2026-11-21 23:56 (`Motion_Graphics_unik`), 2026-11-22 00:12 (`movement_1`), 2026-11-22 00:18 (`movement_2`).

Isi yang relevan untuk kasus yang selama ini blokir: `movement_1.xml` memuat bentuk `.roundrect` berlabel **"Persegi Panjang Bulat 1"** dengan `<location>` berpindah dari `v="0.000000,0.000000,0.000000"` pada `t="0.051819"` ke `v="795.378052,0.000000,0.000000"` pada `t="0.624813"` dengan `e="cubicBezier 0.86685157 0.0 0.43377253 1.0"` — yaitu persegi panjang membulat yang bergerak horizontal dengan easing bezier, tepat bentuk yang dipakai MP-03/PU-03 sebagai bahan.

## Adobe After Effects — `.aep` biner (4 berkas)

| Berkas | Ukuran | Penanda yang terbaca |
|---|---:|---|
| `aep/Motion_Graphics_Unik.aep` | 25.704 B | `dc:format = application/vnd.adobe.aftereffects.project` |
| `aep/Motion_Graphics_Unik_Camera.aep` | 203.068 B | `Camera 1`, `(ADBE Camera Options Group`, `(ADBE Camera Zoom` |
| `aep/movement_1.aep` | 45.416 B | `application/vnd.adobe.aftereffects.project` |
| `aep/movement_2.aep` | 197.708 B | `application/vnd.adobe.aftereffects.project` |

SHA-256:

```
e790748e6d4ce01448b2e5a788ab301160c2f63ef524fa844fa4d418fd4d23f5  aep/Motion_Graphics_Unik.aep
f6269372fd3a7bc894edd3b3b9d520a002e9a745be1d40b3226fde07d00f8e1c  aep/Motion_Graphics_Unik_Camera.aep
7067f17d5c7064a126a53aa2ee3aff1098fa4c2b7acb862862ac753cddca0da6  aep/movement_1.aep
6279b42b92f8f167ec3ededdae92cb28386cfcc677a9b4e765260e9b467a1866  aep/movement_2.aep
```

Keempatnya diawali `52 49 46 58` = **`RIFX`** dengan panjang besar-endian; utilitas `file` menebak "RIFF (big-endian)". Format proyek After Effects bukan XML dan tidak boleh diperlakukan sebagai XML tukar-menukar (AGENTS.md §6).

## Status klaim

| Klaim | Status |
|---|---|
| Ketiga berkas XML adalah ekspor Alight Motion versi 5.0.273.1028425 di Android | **Confirmed** — dibaca langsung dari header/atribut |
| `Motion_Graphics_unik.xml` memuat dua elemen `<camera label="Kamera 1" type="perspective">` dengan `fov 60`, focus-blur dan fog `enabled="false"`, masing-masing di-parent ke `<nullobj label="Nol 1">` terpisah | **Observed in sample** — dibaca sebagai teks dari salinan di repo; tidak ada aplikasi yang dibuka |
| Di format ini kamera dan null object adalah **tipe elemen berbeda** | **Observed in sample** — apakah berlaku pada versi lain tetap **Unverified** |
| `Motion_Graphics_Unik_Camera.aep` mengandung objek kamera dengan grup properti ADBE Camera Options | **Observed in bytes** — string terbaca; **belum** diverifikasi di aplikasi |
| Versi After Effects, daftar comp, jumlah layer, dan nilai keyframe `.aep` | **Not tested** — tidak ada parser, tidak ada akses aplikasi |
| Apakah fitur yang muncul di berkas aktif/berfungsi di proyek | **Unknown** |
| Semua berkas dapat dibuka aplikasi_target tanpa error | **Not tested** |

## Rekaman layar (diserahkan owner, 2026-11-24)

Lokasi: `D:/Download/rekam kamera/`. Tiga berkas MP4, total ±540 MB, **tidak disalin ke repository** karena isinya rekaman layar kerja owner dan ukurannya besar; pencatatan dilakukan lewat path + SHA-256 (lihat [`../fixtures/README.md`](../fixtures/README.md)).

| Berkas | Durasi | Resolusi | Isi yang terverifikasi dari bingkai |
|---|---|---|---|
| `Recording 2026-11-24 070641.mp4` | 00:05:59.40 | 1918×994, 30 fps | Sesi **After Effects**: layer `Camera 1`, grup `Transform` (Point of Interest, Position, Orientation, X/Y/Z Rotation) dan `Camera Options` (Zoom, Depth of Field, Focus Distance, Aperture, Blur Level, Iris Shape = Fast Rectangle) |
| `screen-20261124-215814.mp4` | 00:07:03.65 | 720×1612, ±42,7 fps | **Alight Motion** di Android: menu `Tambahkan` menampilkan **Kamera** dan **Nol** sebagai dua item berbeda; stack layer `Rounded Rectangle 1`, `Transition Copy`, `Rectangle 2`, `Mask 1` |
| `screen-20261124-220101.mp4` | 00:02:18.48 | 720×1612, ±45,3 fps | **Alight Motion**: track `Kamera 1`, panel `Move & Transform`, kurva easing cubic bezier pada panel `Move & Transform`, nilai `960,00 / 540,00 / -1462,77` |

Poin bukti penting untuk PU-04: pada **semua** bingkai yang disampel dari rekaman After Effects (setiap 25 s untuk panel properti, setiap 10 s untuk seluruh UI), **dialog Camera Settings tidak pernah muncul** dan **tidak ada field One-Node / Two-Node** yang terlihat. Status kamera karena itu hanya bisa disimpulkan dari struktur properti (Point of Interest tersedia dan di-keyframe), bukan dibaca langsung dari UI.

## Dampak pada pack lain

Fixture ini memenuhi syarat bahan untuk **PU-03** (pahaman proyek lintas aplikasi) dan sebagian besar syarat **PU-04** (kemampuan spesifik aplikasi). PU-03 kini punya bahan lengkap di `evals/fixtures/` tetapi **belum dijalankan**; PU-04 tetap *blocked* karena **rekaman layar Camera Options belum pernah diserahkan**, dan pengamatan negatif pada rekaman itu tidak bisa digantikan oleh isi berkas XML maupun `.aep`. Ketersediaan bahan adalah langkah pertama, bukan hasil evaluasi.

Konsekuensi spesifik dari isi kamera yang baru diverifikasi: pertanyaan "bedakan objek kamera dari null object" dan "tipe kamera" kini dapat dijawab dari sisi Alight Motion (nilai `type="perspective"` dan elemen `<nullobj>` terpisah, **Observed in sample**). Sisi After Effects tetap butuh rekaman atau akses aplikasi.
