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
