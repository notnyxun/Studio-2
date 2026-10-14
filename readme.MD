# Studio 2 — Klasifikasi Sampah · Kelompok \16/FARID 16 PRO MAX 256 GB NATURAL TITANIUM

Deep Learning (IF25-40401) · Teknik Informatika ITERA · Semester Ganjil 2026/2027

## Anggota Kelompok

| No | Nama Lengkap | NIM | Kontribusi utama |
|---:|---|---|---|
| 1 | BAGAS DWI AJITYA | 123140181 | Setup Project |
| 2 | MUHAMMAD FATAHILLAH FARID | 123140203 | Test Dataset |
| 3 | ADITYA HOT MARTUA SIHITE | 123140114 | Train Dataset |

## Ringkasan Pendekatan

- **Arsitektur / backbone:** ResNet-18 pretrained ImageNet.
- **Strategi pelatihan:** Fine-tuning menggunakan PyTorch dengan 8 epoch dan seed 42. Model terbaik dipilih berdasarkan akurasi validasi lokal.
- **Learning rate, optimizer, scheduler, dan augmentasi:** Mengikuti konfigurasi pada `train_baseline.py`. Detail konfigurasi mengikuti implementasi starter kit yang digunakan.
- **Data tambahan:** Tidak ada data tambahan di luar dataset yang disediakan untuk tugas Studio 2.
- **Ukuran input & preprocessing:** Mengikuti transformasi gambar yang didefinisikan dalam `submission/model.py`.
- **Framework:** PyTorch dan Torchvision.
- **Lingkungan pelatihan:** Google Colab dengan GPU CUDA.

## Hasil

| Putaran | Commit | Macro-F1 (split validasi lokal) | Macro-F1 (diumumkan asisten) |
|---|---|---:|---:|
| Preview 1 (14 Okt) | 0.9255 | — | — |
| Preview 2 (21 Okt) | — | — | — |
| Final (25 Okt) | — | - | — |

**Catatan:** Macro-F1 sebesar 0.9255 dan akurasi 0.9317 diperoleh dari evaluasi lokal pada 410 gambar. Nilai pada kolom Macro-F1 yang diumumkan asisten diisi setelah hasil resmi tersedia. Nilai validasi lokal bukan skor final kompetisi.

### F1-Score per Kelas

| Kelas | F1-Score |
|---|---:|
| `botol_plastik` | 0.9474 |
| `gelas_plastik` | 0.9620 |
| `kertas_kardus` | 0.8462 |
| `saset_kemasan` | 0.9307 |
| `styrofoam` | 0.9412 |

### Catatan Eksperimen

Model ResNet-18 pretrained dilatih selama 8 epoch. Akurasi validasi lokal tertinggi yang tercatat selama training adalah 0.9317 pada epoch ke-3. Bobot model terbaik disimpan ke `submission/model.pth`.

Evaluasi lokal menghasilkan Macro-F1 sebesar 0.9255 dan akurasi sebesar 0.9317. Kelas `kertas_kardus` memiliki F1-Score terendah, yaitu 0.8462, sehingga menjadi kandidat utama untuk perbaikan pada eksperimen berikutnya.

## Cara Reproduksi

Jalankan perintah berikut dari direktori utama repositori.

### 1. Instalasi Dependensi

Pastikan Python, PyTorch, dan Torchvision tersedia. Jika menggunakan `requirements.txt`, instal dengan:

```bash
pip install -r requirements.txt
```

### 2. Training Model

Contoh perintah training menggunakan starter kit:

```bash
python train_baseline.py \
  --data /path/to/dataset/train \
  --epochs 8 \
  --seed 42
```

Ganti `/path/to/dataset/train` dengan lokasi folder `train/` yang benar.

### 3. Evaluasi Model

```bash
python evaluate.py \
  --submission ./submission \
  --data ./my_val \
  --batch-size 32 \
  --out ./evaluation.json
```

Folder `my_val` harus berisi validation set lokal dengan struktur folder kelas yang sesuai. Dataset tidak disertakan dalam repositori.

## Struktur Repositori

```text
.
├── README.md
├── train_baseline.py
├── evaluate.py
└── submission/
    ├── model.py
    └── model.pth
```

- `submission/model.py`: definisi model dan transformasi gambar melalui `get_model()` dan `get_transform()`.
- `submission/model.pth`: bobot `state_dict` model terbaik.
- `train_baseline.py`: skrip pelatihan baseline.
- `evaluate.py`: skrip evaluasi resmi dari starter kit.
- `README.md`: dokumentasi pendekatan, hasil eksperimen, dan cara reproduksi.

## Catatan

- Dataset dan validation set lokal tidak disertakan dalam repositori.
- Skor resmi mengikuti evaluasi asisten pada validation set tersembunyi.
- Seluruh eksperimen dan submission mengikuti ketentuan tugas Studio 2.
