# 40-TECHSTACK — titipo-ai-models

STATUS: defined pending — STUB_UNTIL model pertama disetujui TownHall.

Mengacu: TitipO-TownHall v1.0.0

## 1. Target stack

| Lapisan | Teknologi + versi | Keterangan |
|---|---|---|
| Latih | Python 3.12 + scikit-learn | Rekomendasi vendor dan prediksi permintaan |
| Serving target | Rust axum 0.8.4 + uuid v7 | Selaras pin backend bila model naik produksi |
| Format bobot | ONNX | Tidak ada pickle sembarang di produksi |
| Data | Event titipo-data-pipeline 90 hari anonim | Tanpa PII di repo |
| Klien | Kotlin 2.2.20 + Compose 1.8.2 + Navigation3 1.0.0 | Hanya menampilkan skor, bukan menghitung model |
| Web | Bun 1.4.x + Svelte 5 + Kit 2 + TS 5.9.x | Hanya menampilkan alasan skor di admin |

STUB_UNTIL berarti repo ini belum memengaruhi keputusan produksi; rekomendasi vendor manual via aturan jarak dan riwayat tetap berlaku.

## 2. Konfigurasi kunci

- Tanpa berkas model di atas 10 MB di repo; simpan di object storage dan catat URL + checksum.
- Dataset contoh maksimal 100 baris nama samaran; setiap model wajib kartu: sumber data, metrik, batasan.
- Konsumsi event dari pipeline, bukan akses DB titipo langsung.

## Batasan

- Bukan penentu fee 12 persen, bukan penentu repeat 40 persen, bukan penentu cutoff 20.00 dan serah 06.00–08.00.
- Dilarang mengklaim produksi sebelum STUB_UNTIL dicabut via PR TownHall.
