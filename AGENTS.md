# AGENTS.md — titipo-ai-models

Model AI TitipO (rekomendasi vendor, prediksi permintaan) beserta model card; berstatus stub sampai model pertama disetujui TownHall.

Divisi TitipO (Epic E2 [#3](https://github.com/Coding-Skuy/ChefGenie-TownHall/issues/3), milestone v1.0.0). Bahasa semua artefak: Indonesia.

## Sumber kebenaran

Dokumen beku v1.0.0 ada di repo [TitipO-TownHall](https://github.com/Coding-Skuy/TitipO-TownHall). Repo ini hanya menjalankan, bukan mendefinisikan, requirement.

| Dokumen | Isi | Link |
|---|---|---|
| `platform/versions/v1.0.0/BRD/00-ikhtisar.md` | Ikhtisar bisnis, vendor kurasi, titip harian, fee | [buka](https://github.com/Coding-Skuy/TitipO-TownHall/blob/main/platform/versions/v1.0.0/BRD/00-ikhtisar.md) |
| `platform/versions/v1.0.0/PRD/10-pengguna.md` | Pengguna dan kebutuhan | [buka](https://github.com/Coding-Skuy/TitipO-TownHall/blob/main/platform/versions/v1.0.0/PRD/10-pengguna.md) |
| `platform/versions/v1.0.0/FRD/10-fungsional.md` | Kebutuhan fungsional FR-001..FR-304 | [buka](https://github.com/Coding-Skuy/TitipO-TownHall/blob/main/platform/versions/v1.0.0/FRD/10-fungsional.md) |
| `platform/versions/v1.0.0/SRS/30-non-functional.md` | Non-fungsional (kinerja, keamanan, rollback) | [buka](https://github.com/Coding-Skuy/TitipO-TownHall/blob/main/platform/versions/v1.0.0/SRS/30-non-functional.md) |
| `platform/versions/v1.0.0/SRS/40-acceptance-criteria.md` | Kriteria penerimaan QA gate | [buka](https://github.com/Coding-Skuy/TitipO-TownHall/blob/main/platform/versions/v1.0.0/SRS/40-acceptance-criteria.md) |
| `metrik/10-repeat-order.md` | Metrik repeat-order (living) | [buka](https://github.com/Coding-Skuy/TitipO-TownHall/blob/main/metrik/10-repeat-order.md) |
| `vendor/10-sla-vendor.md` | SLA vendor (living) | [buka](https://github.com/Coding-Skuy/TitipO-TownHall/blob/main/vendor/10-sla-vendor.md) |
| `KONTEKS-LINTAS-DIVISI.md` | Konteks lintas-divisi (event registry, ID, satuan, metrik) | [buka](https://github.com/Coding-Skuy/ChefGenie-TownHall/blob/main/KONTEKS-LINTAS-DIVISI.md) |
| `townhall-roadmap.md` | Epic E2 #3, milestone v1.0.0, Definisi Selesai §6 | [buka](https://github.com/Coding-Skuy/ChefGenie-TownHall/blob/main/townhall-roadmap.md) |

Aturan:
- Dilarang menduplikasi requirement di repo kode; cukup tautkan ke versi di atas.
- Requirement berubah = PR di TitipO-TownHall dahulu (versi baru), baru kode mengikuti.
- Bila dokumen divisi bertentangan dengan KONTEKS-LINTAS-DIVISI.md, laporkan; jangan memperbaiki diam-diam.

## Tech stack terkunci

- Python 3.12 + scikit-learn untuk training; bobot dalam format ONNX; serving via API Rust (axum 0.8.4 + uuid v7, selaras backend).
- Wajib per model: model card (sumber data, metrik eval, batasan) + versi model; berkas model di atas 10 MB tidak masuk repo (object storage + checksum).
- Data: event anonim 90 hari dari `titipo-data-pipeline`; dilarang PII; dataset contoh maksimal 100 baris nama samaran.
- Dilarang: pickle di produksi, akses DB titipo langsung, mengklaim produksi sebelum STUB_UNTIL dicabut lewat PR TownHall.

Angka bisnis TitipO yang berlaku di seluruh repo: fee vendor 12% (+0,5% Prioritas), ongkir flat Rp5.000 (Rp4.000 vendor + Rp1.000 kas), pesan maksimal 20.00, serah 06.00-08.00, pokok ke Lumbung tiap Senin, denda batal sepihak Rp15.000, maksimal 50 kg per transaksi (di atasnya ditandai grosir), ID pesanan `T-2026-NNNNNN`.

## Aturan kerja AI

a. Baca AGENTS.md ini dan seluruh ADR di `docs/decisions/` sebelum menulis kode.
b. TDD merah-hijau: tulis test yang gagal dahulu. Rilis diblokir bila QA gate (SRS/40-acceptance-criteria.md) gagal.
c. Kontrak API/event hanya diubah lewat bump versi + catatan di ADR baru.
d. Pesan commit berawalan `docs:`, `feat:`, atau `fix:`; wajib memperbarui `CHANGELOG.md` repo ini.
e. Keputusan arsitektur baru = tambah ADR bernomor di `docs/decisions/`; jangan mengedit ADR lama (immutable, sama seperti aturan versi TownHall).
f. Dilarang menyentuh DB divisi lain (DB per service; Titeny read-only).
g. Khusus repo ini:
- Model bukan penentu fee 12%, repeat 40%, cutoff 20.00, atau jendela serah 06.00-08.00.

## Definisi selesai

- Dokumen versi lengkap (BRD/PRD/FRD/FSD/SRS) + `SNAPSHOT-ROADMAP.md`.
- QA gate berbasis SRS lulus (TDD merah-hijau).
- Kontrak API terbit; audit keamanan bersih (JWT audiens + DB per service).
- Bukti metrik lintas-divisi (KONTEKS §7) tercatat.
- CHANGELOG versi diperbarui; dokumen beku tidak diedit.
Sumber: [townhall-roadmap.md §6](https://github.com/Coding-Skuy/ChefGenie-TownHall/blob/main/townhall-roadmap.md)
