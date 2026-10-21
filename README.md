# Credit Risk Prediction: End-to-End Machine Learning Project

## Project Overview

Proyek ini bertujuan mengembangkan model machine learning
untuk mengidentifikasi risiko gagal bayar pinjaman berdasarkan
data historis Lending Club periode 2007–2014.

Metodologi pengembangan mengikuti pendekatan CRISP-DM.

## Business Objective

Membangun model klasifikasi biner yang dapat membantu
mengidentifikasi pinjaman dengan risiko gagal bayar lebih tinggi.

Target:
- Good (0): Pinjaman yang telah dilunasi.
- Bad (1): Pinjaman dengan status gagal bayar atau charged off.

Status pinjaman yang belum memiliki hasil final tidak
digunakan dalam pelatihan model.

## Dataset

- Sumber: data pinjaman Lending Club, periode 2007–2014
- Total data mentah: 466,285 baris
- Data berlabel: 230,795 baris
- Jumlah fitur model: 27
- Bad rate keseluruhan: 19.09%

Dataset **tidak disertakan** di repositori ini karena ukurannya
(sekitar 229 MB) melebihi batas file GitHub. Salinan untuk
memudahkan reproduksi tersedia di OneDrive (gunakan tombol
Download, karena file berukuran besar):

- [loan_data_2007_2014.csv](https://1drv.ms/x/c/8C8890B7A4B0A953/IQCtbbpgC1MZS7IZZtXY56YPAWAg_j2bq0fL02JPSuSuj3M?e=Ez3DXO)
- [LCDataDictionary.xlsx](https://1drv.ms/x/c/8C8890B7A4B0A953/IQCY53RepYwlQpmB9hiD96xzAYUNeA6fEphB3XSFaq7-mZQ?e=CJwtgc)

Lihat bagian [Cara Menjalankan](#cara-menjalankan) untuk
menempatkan file data secara lokal.

## Methodology

1. Business Understanding
2. Data Understanding
3. Data Preparation
4. Modeling
5. Evaluation
6. Model Interpretation
7. Deployment & Documentation

## Data Splitting

Pembagian dataset dilakukan secara kronologis:

- Train: 168,010 baris
- Validation: 30,680 baris
- Test: 32,105 baris

Pendekatan ini digunakan untuk mengurangi risiko
kebocoran informasi antarperiode.

## Modeling

Model yang dibandingkan:
- Dummy Classifier
- Logistic Regression
- Random Forest Classifier

Model terpilih: **Random Forest**

Threshold klasifikasi: **0.4948**

Threshold ditentukan pada validation set dengan
batas recall minimum 65%.

## Final Test Performance

| Metric | Value |
|---|---:|
| ROC-AUC | 0.6894 |
| Average Precision | 0.3488 |
| Precision | 30.83% |
| Recall | 65.63% |
| F1-score | 41.95% |
| Accuracy | 62.63% |

## Model Interpretation

Permutation importance dihitung menggunakan
validation set dengan metrik Average Precision.

Lima fitur teratas:

- term: 0.07423
- annual_inc: 0.02584
- dti: 0.01652
- revol_util: 0.00803
- tot_cur_bal: 0.00707

Feature importance menunjukkan kontribusi prediktif,
bukan hubungan sebab-akibat.

## Limitations

- Dataset bersifat historis, mencakup periode 2007–2014.
- Hanya pinjaman dengan status final yang digunakan
  untuk pelatihan dan evaluasi.
- Dataset dapat mengalami selection bias dan perubahan
  karakteristik risiko antarperiode.
- Probabilitas model belum melalui proses kalibrasi khusus.
- Threshold merupakan asumsi evaluasi proyek,
  bukan kebijakan kredit institusi.
- Ketersediaan fitur pada waktu keputusan kredit,
  khususnya term dan variabel kredit lainnya,
  perlu diverifikasi sebelum penerapan operasional.
- Model belum divalidasi menggunakan data eksternal terbaru.
- Model tidak ditujukan sebagai sistem persetujuan
  atau penolakan kredit secara otomatis.

## Technology Stack

Python, Pandas, NumPy, Matplotlib, Seaborn,
scikit-learn, Jupyter Notebook, dan joblib.

## Struktur Repositori

```
.
├── credit-risk-analyst.ipynb   Notebook utama (Step 1 sampai Step 7)
├── data/                       Tempat file data (tidak disertakan di repo)
├── models/                     Model terlatih dan konfigurasinya
├── outputs/                    Hasil tiap tahap (CSV dan konfigurasi)
├── reports/                    Presentasi proyek
├── requirements.txt
└── README.md
```

## Model Artifacts

- `models/credit_risk_random_forest_v2.joblib`
- `models/credit_risk_model_config_v2.json`

Model disimpan dengan joblib dan sebaiknya dimuat dengan versi
scikit-learn yang sama seperti pada `requirements.txt`.

## Cara Menjalankan

1. Buat dan aktifkan virtual environment, lalu pasang dependensi:

   ```
   python -m venv .venv
   .venv\Scripts\activate
   pip install -r requirements.txt
   ```

2. Unduh `loan_data_2007_2014.csv` dan `LCDataDictionary.xlsx`
   dari link di bagian Dataset, lalu letakkan di folder `data/`.

3. Buka `credit-risk-analyst.ipynb` dan jalankan sel secara
   berurutan mulai dari Step 1 hingga Step 7.

## Reproducibility

Random state: 42

## Presentasi

Ringkasan proyek dalam bentuk slide:
[credit_risk_prediction_portfolio.pptx](https://1drv.ms/p/c/8C8890B7A4B0A953/IQDf30yn_tHVSJLVxNbAVqZHATIify3DV-vjHl3txwLzqGg?e=b1SRxo)
