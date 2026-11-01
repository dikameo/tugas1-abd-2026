# Data Tugas 1

## Dataset yang Dipilih

Isi informasi berikut sebelum Milestone 1.

| Item | Isi |
|---|---|
| Nama dataset | `[MedFact-Synth]` |
| Sumber | `[https://huggingface.co/datasets/Xingchi888/MedFact-Synth (duplikat dari nlm-dir/MedFact-Synth)]` |
| Lisensi/ketentuan pakai | `[MIT]` |
| Ukuran | `[1.497.981 baris; 17 file Parquet (train-00000 s.d. train-00016 of 00017), ~3,3 GB]` |
| Periode data | `[Artikel PubMed baseline 2025; dataset dirilis Maret 2026 (tanpa kolom tanggal)]` |
| Unit analisis | `[Pasangan klaim biomedis dan artikel sumber (PubMed) beserta skor kesesuaian -2 s.d. 2 (synthetic_label)]` |

Kolom: `idx`, `claim_pmid`, `claim_potential`, `claim`, `source_pmid`, `source`, `synthetic_label`, `system_prompt`, `user_prompt`, `assistant_prompt`.

## Dataset Time Series: PEMS-BAY

Dataset ini dipakai oleh `notebooks/01_data_profiling_timeseries.ipynb` untuk analisis deret waktu dan spasial.

| Item | Isi |
|---|---|
| Nama dataset | `PEMS-BAY` (data lalu lintas jalan raya San Francisco Bay Area) |
| Sumber | https://huggingface.co/datasets/witgaw/PEMS-BAY (turunan dari dataset PEMS-BAY pada paper DCRNN, Li dkk., ICLR 2018) |
| Lisensi/ketentuan pakai | MIT. Jika dipakai, sitasi paper DCRNN: *Diffusion Convolutional Recurrent Neural Network: Data-Driven Traffic Forecasting* |
| Ukuran | 16.930.225 baris x 50 kolom; 3 file Parquet (`train.parquet` 344 MiB, `val.parquet` 49 MiB, `test.parquet` 98 MiB), total ±491 MiB (±515 MB) |
| Periode data | 2017-01-01 00:55 s.d. 2017-06-30 22:55, resolusi 5 menit (52.093 timestamp unik) |
| Unit analisis | Satu sensor pada satu waktu referensi `t0`: 12 langkah kecepatan ke belakang (`x_*`) dan 12 langkah target ke depan (`y_*`) |
| Cakupan ruang | 325 sensor (`node_id` 0-324) dengan koordinat pada `sensor_graph/sensor_locations.csv` |

Kolom:

- `node_id`: identitas sensor (0-324), dipetakan ke `sensor_id` lewat `sensor_graph/adj_mx_mapping.json`.
- `t0_timestamp`: waktu referensi (String ISO 8601, perlu di-parse ke `Datetime`).
- `x_t-11_d0` ... `x_t+0_d0` dan `y_t+1_d0` ... `y_t+12_d0`: kecepatan lalu lintas (mph). Nilai `0` menandai pembacaan sensor yang hilang.
- `x_t-11_d1` ... `x_t+0_d1` dan `y_t+1_d1` ... `y_t+12_d1`: waktu dalam hari (dinormalisasi 0-1).

Pembagian data bersifat kronologis: `train` (2017-01-01 s.d. 2017-05-07), `val` (2017-05-07 s.d. 2017-05-25), dan `test` (2017-05-25 s.d. 2017-06-30).

Cara memperoleh data: jalankan cell unduh pada `notebooks/01_data_profiling_timeseries.ipynb`, yang menyimpan berkas ke `data/raw/pems-bay/`. Secara manual:

```python
from huggingface_hub import snapshot_download

snapshot_download(
    'witgaw/PEMS-BAY', repo_type='dataset', local_dir='data/raw/pems-bay',
    allow_patterns=['*.parquet', 'sensor_graph/sensor_locations.csv', 'sensor_graph/adj_mx_mapping.json'],
)
```

Catatan: dataset ini berasal dari California, Amerika Serikat, bukan dataset Indonesia seperti yang diminta pada spesifikasi tugas.

## Tempat Mencari Dataset

Pilih dataset Indonesia yang legal digunakan, dapat didokumentasikan sumbernya, dan memenuhi batas ukuran tugas.

| Situs | Kegunaan |
|---|---|
| [Satu Data Indonesia](https://data.go.id/) | Portal data terbuka lintas instansi pemerintah Indonesia. |
| [Badan Pusat Statistik](https://www.bps.go.id/) | Statistik sosial, ekonomi, kependudukan, dan data wilayah. |
| [BMKG Data Online](https://dataonline.bmkg.go.id/) | Data cuaca, iklim, gempa bumi, dan observasi meteorologi. |
| [Hugging Face Datasets](https://huggingface.co/datasets) | Dataset publik yang dapat dicari berdasarkan topik, bahasa, atau ukuran. |
| [Kaggle Datasets](https://www.kaggle.com/datasets) | Katalog dataset publik; periksa lisensi dan dokumentasi pembuatnya. |
| [Google Dataset Search](https://datasetsearch.research.google.com/) | Mesin pencari untuk menemukan dataset dari berbagai portal. |

## Cara Memperoleh Data

1. Buka URL sumber di atas.
2. Unduh file ke folder `data/raw/` tanpa mengubah data mentah.
3. Catat nama file dan checksum bila tersedia.
4. Ubah variabel `DATA_PATH` pada `notebooks/01_data_profiling.ipynb` agar menunjuk ke file tersebut.

## Aturan Penyimpanan

- Jangan commit dataset mentah atau hasil olahan berukuran besar ke Git.
- File pada `data/raw/` adalah data asli dan tidak boleh diubah.
- Simpan hasil transformasi yang dapat direproduksi pada `data/processed/`.
