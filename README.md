# TitipO AI Models — Divisi TitipO (Community Commerce)

> **STATUS: stub — fase nanti.** Belum ada model terlatih di repo ini.
> TownHall: [TitipO-TownHall](https://github.com/Coding-Skuy/TitipO-TownHall).
> Auth/kontrak data mengikuti pola Lumbung: [Lumbung-TownHall](https://github.com/Coding-Skuy/Lumbung-TownHall).

## Rencana fase nanti

1. **Rekomendasi vendor** — ranking vendor keliling per rumah tangga berdasar jarak, jadwal, riwayat titip.
2. **Prediksi permintaan harian** — estimasi jumlah titipan per rute agar vendor membawa stok tepat.
3. **Deteksi anomali pesanan** — pesanan ganda / pola batal berulang.

## Kebijakan

- Tanpa data PII di repo. Contoh data memakai nama samaran.
- Setiap model wajib mencantumkan: sumber data, metrik, batasan.
- Konsumsi event dari `titipo-data-pipeline` (event pesanan → Titeny), bukan akses DB langsung.

## Struktur

```text
models/README.md   # katalog model + format kartu model
```

## Tautan

- TownHall: https://github.com/Coding-Skuy/TitipO-TownHall
- Pipeline: https://github.com/Coding-Skuy/titipo-data-pipeline
- Backend: https://github.com/Coding-Skuy/titipo-backend-service
