# ADR-0001 — Fondasi teknis titipo-ai-models

Status: Diterima | Tanggal: 2026-10-14

## Konteks

titipo-ai-models adalah bagian divisi TitipO (Epic E2 #3, milestone v1.0.0). Spesifikasi v1.0.0 beku sejak 2026-10-07 di [TitipO-TownHall](https://github.com/Coding-Skuy/TitipO-TownHall/blob/main/platform/versions/v1.0.0/FSD/30-kontrak.md). Repo ini memerlukan fondasi teknis yang tetap agar pengembangan oleh AI dan manusia konsisten.

## Keputusan

Keputusan kunci CEO yang berlaku untuk repo ini:

1. **Stack AI terkunci.** Training Python 3.12 + scikit-learn, bobot ONNX, serving lewat API Rust; tidak ada serving Python di produksi.
2. **Model card wajib.** Setiap model memuat model card, metrik eval, dan versi model; rilis tanpa itu ditolak.
3. **STUB_UNTIL.** Repo belum memengaruhi keputusan produksi; rekomendasi vendor tetap aturan jarak dan riwayat sampai persetujuan TownHall.
4. **Tanpa PII dan tanpa akses DB.** Data latih hanya dari event pipeline yang dianonimkan; tidak ada akses langsung ke DB titipo.

Keputusan lintas repo: satu DB logis per service, JWT beraudien divisi, kunci idempoten ULID klien pada semua POST, uang integer rupiah, waktu timestamptz UTC.

## Konsekuensi

Naik produksi menunggu PR TownHall yang mencabut STUB_UNTIL. Mundur: matikan flag saran dan kembali ke urutan jarak terdekat.
ADR ini immutable; perubahan keputusan ditulis sebagai ADR baru yang menggantikan.
