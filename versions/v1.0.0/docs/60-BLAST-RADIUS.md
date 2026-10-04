# 60-BLAST-RADIUS — titipo-ai-models

## Konsumen

- Konsumen langsung: belum ada di produksi (STUB_UNTIL); calon konsumen `titipo-web` (tampilan skor) dan `titipo-app-kmp` (urutan vendor).
- Hulu: `titipo-data-pipeline` (event pesanan anonim 90 hari).
- Hilir: tidak ada tulis ke DB titipo; hanya saran baca.

## Failure

- Model salah peringkat: vendor jauh naik ke atas; mitigasi batas STUB_UNTIL sehingga produksi tetap memakai aturan jarak dan riwayat.
- Data latih bocor PII: tolak dataset; putar ulang dengan nama samaran; audit 100 baris contoh.
- Bobot besar masuk repo: tolak PR; pindah ke object storage dengan checksum.
- Serving Rust tidak cocok versi: kunci axum 0.8.4 dan uuid v7 disamakan dengan backend sebelum naik.

## Rollback

- Rollback berarti matikan flag saran dan kembali ke urutan manual jarak terdekat; tidak ada migrasi data.
- STUB_UNTIL aktif kembali bila metrik CTR pilihan di bawah 25 persen selama 2 minggu.
- Tidak ada rollback secret karena repo tidak menyimpan service key.

## Batasan

- Dampak maksimal urutan saran; tidak menyentuh pesanan, fee, ledger, atau auth JWT beraudien titipo.
- Insiden data dieskalasi ke pemilik pipeline dan TownHall, bukan perbaikan bobot diam-diam.
