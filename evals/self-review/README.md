# Self Review — Evaluasi Mandiri Kontribusi Agent

**Status:** Dijalankan 2026-11-24. Rata-rata awal **88,0 / 100** dari 6 kasus; lima lulus, **SR-05 = 78/100 gagal ambang** (metode evaluasi dinilai diri sendiri oleh penulis skill). Adendum Review 006 (hari yang sama) menilai ulang SR-06 dari 90 ke 93 sehingga rata-rata menjadi **88,5 / 100**; catatan asli tetap utuh di berkas hasil. Tidak ada critical failure.

Pack ini menilai **pekerjaan saya** pada kelanjutan repository — bukan perilaku sebuah skill. Pack lain (`project-understanding`, `motion-graphics-principles`) mengukur apakah sebuah skill menghasilkan keluaran yang benar; pack ini mengukur apakah agen yang menulis dan menilai itu bekerja dengan benar.

Bahasa: Indonesia, atas permintaan owner. Konvensi dokumen teknis repository tetap Inggris; istilah teknis, nama berkas, dan nama kasus dibiarkan Inggris.

## Batasan yang harus dibaca sebelum mempercayai skor ini

Penilai adalah agen yang sama yang mengerjakan dan yang memberi skor. Ini cacat struktural, bukan formalitas, sehingga pack ini punya aturan tambahan:

1. **Setiap skor wajib menunjuk bukti yang bisa diperiksa ulang oleh owner** — path berkas, perintah, dan nilai yang diharapkan. Skor tanpa perintah reproduksi tidak boleh dicatat.
2. **Kekurangan dicatat dengan angka, bukan disembunyikan di narasi.** SR-05 sengaja dinyatakan gagal.
3. Klaim eksekusi hanya berlaku untuk perintah yang benar-benar dijalankan pada tanggal yang dicatat.

Mitigasi kontaminasi pada pack perilaku (agent dilarang membuka `evals/`) bersifat **imbauan, bukan paksaan** — agen punya akses baca ke seluruh repository. Ini dicatat sebagai kekurangan di SR-05, bukan sebagai keunggulan.

## Cara menjalankan ulang

```bash
# 1. Validasi struktural
python tests/validate_skills.py          # harapan: PASS, 7 skill
bash tests/test_count_extensions.sh      # harapan: PASS

# 2. Inventaris fixture aplikasi (lihat fixture-inventory.md untuk nilai harapan)
sha256sum "D:/Download/update/XML/"*.xml "D:/Download/update/aep/"*.aep

# 3. Nilai ulang tiap kasus pada results/assessment-2026-11-24.md
#    dengan scorecard.md, lalu bandingkan terhadap catatan tanggal ini.
```

## Isi pack

| Berkas | Isi |
|---|---|
| [`cases.md`](cases.md) | Enam kasus: SR-01 … SR-06, masing-masing dengan bukti dan perintah pemeriksaan |
| [`scorecard.md`](scorecard.md) | Dimensi, bobot, ambang, dan critical failure yang saya susun sendiri |
| [`fixture-inventory.md`](fixture-inventory.md) | Data terverifikasi dari `D:/Download/update` (hash, versi aplikasi, census keyframe) |
| [`results/assessment-2026-11-24.md`](results/assessment-2026-11-24.md) | Skor, bukti, kekurangan, dan keputusan |

## Aturan lulus

Sama seperti pack lain di repository: kasus lulus pada **≥ 80/100 tanpa critical failure**. Rata-rata pack dilaporkan, tetapi keputusan perbaikan diambil per kasus — angka agregat tidak menutupi satu kasus gagal.

## Tautan

- [`../README.md`](../README.md) — matriks status seluruh evaluation pack
- [`../project-understanding/review-log.md`](../project-understanding/review-log.md) — Review 005 mencatat hasil pack ini
