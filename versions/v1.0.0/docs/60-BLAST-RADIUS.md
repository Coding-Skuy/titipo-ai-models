# 60-BLAST-RADIUS — titipo-ai-models

> Versi: v1.0.0 | Status: disetujui | Menggantikan: -
> Acuan: [TitipO-TownHall platform/versions/v1.0.0](https://github.com/Coding-Skuy/TitipO-TownHall/tree/main/platform/versions/v1.0.0) (BRD/PRD/FRD/FSD/SRS beku 2026-10-07).

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

## Boleh disentuh

Notebook/skrip training, model card, metrik eval, spesifikasi serving ONNX, dataset contoh 100 baris samaran.

## Dilarang

PII, bobot di atas 10 MB di repo, akses DB titipo, mengklaim produksi sebelum STUB_UNTIL dicabut, menentukan fee/repeat/cutoff.

## Kontrak yang dikonsumsi

Event anonim 90 hari dari `titipo-data-pipeline`.

## Kontrak yang diproduksi

Skor rekomendasi vendor lewat API Rust (kelak); saran baca saja.

Sumber batas: [townhall-roadmap.md §2](https://github.com/Coding-Skuy/ChefGenie-TownHall/blob/main/townhall-roadmap.md) baris TitipO (pesan <=20.00, serah 06.00-08.00; sinyal `pedaree.stok.v1` anjuran saja; fee vendor 12%) dan [KONTEKS-LINTAS-DIVISI.md](https://github.com/Coding-Skuy/ChefGenie-TownHall/blob/main/KONTEKS-LINTAS-DIVISI.md) §3, §8, §9.
