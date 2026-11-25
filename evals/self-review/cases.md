# Self Review — Kasus

Setiap kasus menilai satu aspek kontribusi agen pada 2026-11-24. Bukti, bukan kesan: tiap kasus punya perintah pemeriksaan.

## SR-01 — Kelengkapan kontinuitas repository

**Pertanyaan:** Apakah seluruh yang diminta owner ("keseluruhan kelanjutan repository lengkap") benar-benar ada di dalam tree?

**Periksa:**

```bash
ls skills/                                    # harapan: 7 direktori skill
ls evals/motion-graphics-principles/           # harapan: README.md cases.md scorecard.md results/
find . -type f | wc -l                         # harapan: 54 (per 2026-11-24, sebelum pack ini)
```

**Catatan bobot:** `evals/motion-graphics-principles/scorecard.md` semula tertulis **di luar** tree (`Downloads/motion-graphics-ai-handoff-v1.0 (1)/motion-graphics-ai-framework/...`), sehingga pack yang dilaporkan "siap" sebenarnya tidak lengkap. Ditemukan saat pemeriksaan ulang, bukan saat penulisan.

## SR-02 — Integritas klaim dan bukti

**Pertanyaan:** Adakah klaim hasil yang tidak didukung eksekusi sendiri?

**Periksa:** `evals/project-understanding/review-log.md` Review 003 dan Review 004 — setiap baris `PASS` harus punya perintah yang setara di bagian "Validation performed".

**Catatan bobot:** Pada awal sesi, dua hasil `PASS` (validator dan helper) dilaporkan dari review-log, bukan dari eksekusi; kemudian benar-benar dijalankan. Perbedaan "dikutip" vs "dijalankan" tidak langsung dinyatakan ke owner. `Relative Markdown-link check` dicatat **not run** daripada diklaim lulus.

## SR-03 — Privasi, keamanan, dan preservasi data

**Pertanyaan:** Apakah berkas asli pengguna tetap utuh dan tidak ada data yang bocor?

**Periksa:**

```bash
git status --porcelain | head        # dari root handoff; tree referensi harus tidak berubah
diff -q reference-repository/motion-graphics-ai-framework/skills/project-understanding/SKILL.md \
        workspace/motion-graphics-ai-framework/skills/project-understanding/SKILL.md   # harapan: berbeda (kerja ada di salinan)
```

**Catatan bobot:** Seluruh penulisan terjadi di `workspace/`; `reference-repository/` dan ZIP tidak disentuh. Satu perintah `mv` + `rm -rf` untuk membereskan tree nyasar diajukan sebelum owner menyetujuinya — meskipun tree itu buatan saya sendiri, langkah pertama seharusnya salin-lalu-minta, bukan hapus.

## SR-04 — Validasi teknis dan konsistensi dokumen

**Periksa:**

```bash
python tests/validate_skills.py
bash tests/test_count_extensions.sh
wc -l skills/project-understanding/SKILL.md      # harapan < 500 (222)
```

**Pertanyaan tambahan:** Apakah README, AGENTS.md, SKILL-ARCHITECTURE.md, dan peta `evals/` cocok dengan isi disk saat ini?

## SR-05 — Validitas metode evaluasi perilaku

**Pertanyaan:** Apakah skor PU-01/02/05 dan MP-01/02/03 layak dipercaya sebagai bukti?

**Periksa:** tiap `results/*/prompt.md` harus memuat klien, tanggal, revisi skill, dan kondisi; tiap `response.md` harus utuh; tiap `evaluation.md` harus punya tabel dimensi dan checklist perilaku.

**Uji kontaminasi yang gagal ditutup rapat:**

```bash
# Agen dijalankan dengan imauan "jangan buka evals/", tetapi konteks agen punya akses baca:
grep -R "evals/" evals/project-understanding/results/PU-05/retest-2026-11-24.md | head -3
```

**Fokus kelemahan:** penilai = penulis skill; satu keluarga klien/model; tidak ada reviewer manusia; MP-01 dan MP-03 tidak di-run ulang setelah revisi.

## SR-06 — Penanganan fixture aplikasi yang baru disediakan

**Pertanyaan:** Ketika owner menyerahkan proyek asli (`D:/Download/update`), apakah identitas, versi, dan batasannya ditetapkan dengan benar — dan apakah berkas itu diproses dengan hormat?

**Periksa:** [`fixture-inventory.md`](fixture-inventory.md) dan jalankan ulang perintah di file itu.

**Aturan yang berlaku:** `AGENTS.md` §11 — proyek pribadi pengguna, media proprietary, dan rekaman tidak boleh di-commit tanpa izin eksplisit dan dasar lisensi. Karena itu fixture **tidak disalin** ke repository; yang dicatat hanya path, ukuran, SHA-256, dan properti yang terbaca.
