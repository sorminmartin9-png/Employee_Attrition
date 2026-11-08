# Employee Attrition (A09) - UTS Milestone 1, IF2116 Pembelajaran Mesin

Memprediksi karyawan yang berisiko resign (klasifikasi biner) menggunakan dataset IBM HR Analytics, dengan fokus pada validasi yang benar, perbandingan model, dan pelaporan yang jujur.

- Kelompok: Employe Attrition
- Anggota: Martin Sormin
- Project ID: A09 

## Struktur repositori

```
.
├── README.md
├── requirements.txt
├── employee_attrition_milestone1_kelompok_09.ipynb   <- notebook utama UTS (Milestone 1)
├── Laporan_UTS_Milestone1_A09.pdf                    <- laporan UTS
└── lampiran/                                         <- notebook eksperimen tambahan
    ├── employee_attrition_pertemuan5.ipynb           (validasi, kestabilan, ensemble, imbalance)
    └── employee_attrition_pertemuan6.ipynb           (PCA dan clustering)
```

Angka pada laporan bagian H dan log eksperimen (run 1 sampai 7) berasal dari notebook utama. Run 8 sampai 10 dan paragraf "Eksperimen tambahan" di laporan berasal dari notebook di folder `lampiran/`.

## Dataset

IBM HR Analytics Employee Attrition & Performance (Kaggle). Data hipotetis buatan data scientist IBM, 1.470 baris dan 35 kolom, target `Attrition`.

- URL: https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset
- File: `WA_Fn-UseC_-HR-Employee-Attrition.csv`
- Dataset tidak disertakan di repositori karena milik pihak lain.

Cara memperoleh: buka URL di atas, login ke Kaggle (gratis), klik Download, ekstrak zip, lalu ambil file CSV tanpa mengubah namanya.

### Versi data

- 227.977 byte, 1.470 baris x 35 kolom (1.233 No dan 237 Yes).
- MD5: `ad8207459e5732574372cf8ff619883f`.
- Cek di komputer Anda: Windows `certutil -hashfile WA_Fn-UseC_-HR-Employee-Attrition.csv MD5`; Linux atau macOS `md5sum WA_Fn-UseC_-HR-Employee-Attrition.csv`. Hasil sama berarti data identik.
- File mentah tidak pernah diubah; seluruh pembersihan dilakukan di dalam kode.

## Cara menjalankan

1. Buka notebook di Google Colab (File, Upload notebook) atau Jupyter.
2. Unggah `WA_Fn-UseC_-HR-Employee-Attrition.csv` saat sel pemuatan data meminta, atau taruh di folder yang sama dengan notebook.
3. Pilih Runtime, Restart session and run all.
4. Hasil yang benar: sel pemuatan data mencetak ukuran `(1470, 35)`. Seed: `RANDOM_STATE = 42`.

## Lingkungan

Python 3.13.18 (Google Colab), numpy 2.4.6, pandas 2.2.3, scikit-learn 1.6.1 (dicetak oleh sel versi di notebook utama). Daftar lengkap ada di `requirements.txt`.

## Metodologi singkat

- Pembagian data stratified 80:20 (1.176 training dan 294 test). Test set tidak dipakai untuk EDA, pemilihan model, maupun tuning pada Milestone 1.
- Perbandingan model dengan Stratified 5-Fold CV pada data training.
- Imputasi, scaling, dan one-hot encoding di dalam Pipeline agar tidak terjadi data leakage.
- Metrik utama: F1 dan Recall kelas resign (kelas resign hanya 16,12%). Standar deviasi pada tabel adalah standar deviasi populasi (ddof = 0), sesuai perhitungan di notebook.

## Hasil validasi awal (5-fold CV pada data training, rata-rata ± standar deviasi)

| Model | F1 | Recall | Precision | ROC-AUC | Gap F1 (train - CV) |
|---|---|---|---|---|---|
| Dummy (mayoritas) | 0,000 ± 0,000 | 0,000 ± 0,000 | 0,000 ± 0,000 | 0,500 ± 0,000 | 0,000 |
| Logistic Regression | 0,561 ± 0,098 | 0,442 ± 0,096 | 0,776 ± 0,074 | 0,839 ± 0,029 | 0,051 |
| LR + class_weight | 0,492 ± 0,034 | 0,737 ± 0,062 | 0,372 ± 0,038 | 0,827 ± 0,028 | 0,058 |
| KNN (k=15) | 0,058 ± 0,077 | 0,032 ± 0,042 | 0,400 ± 0,490 | 0,746 ± 0,057 | 0,060 |
| Decision Tree (depth=5) | 0,370 ± 0,085 | 0,305 ± 0,098 | 0,488 ± 0,045 | 0,666 ± 0,077 | 0,258 |
| Random Forest | 0,321 ± 0,078 | 0,205 ± 0,065 | 0,872 ± 0,138 | 0,815 ± 0,034 | 0,679 |
| Gradient Boosting | 0,451 ± 0,075 | 0,332 ± 0,072 | 0,731 ± 0,085 | 0,813 ± 0,016 | 0,445 |

Kesimpulan sementara: Logistic Regression dengan fitur asli + turunan (F1 0,589; ROC-AUC 0,847) menjadi kandidat utama, dan LR + class_weight (Recall 0,732) menjadi alternatif jika prioritasnya menangkap sebanyak mungkin karyawan yang berpotensi resign. Model final belum ditetapkan.

## Log eksperimen

| Run | Eksperimen | Hasil kunci | Keputusan |
|---|---|---|---|
| 1 | Logistic Regression | F1 0,561; Recall 0,442 | Baseline model |
| 2 | Random Forest | F1 0,321; Recall 0,205 | Kalah dari baseline; overfitting berat (gap 0,679) |
| 3 | LR + class_weight | F1 0,492; Recall 0,737 | Recall naik, Precision turun |
| 4 | KNN, Decision Tree, Gradient Boosting | F1 0,058; 0,370; 0,451 | Tidak melampaui Logistic Regression |
| 5 | Fitur turunan pada Logistic Regression | F1 0,561 menjadi 0,589 | Selisih tidak bermakna; dipertahankan pada kandidat utama |
| 6 | Random Forest teregularisasi | F1 0,464; Recall 0,395; gap 0,405 | Gap turun, tetap di bawah Logistic Regression |
| 7 | Eksplorasi threshold (LR + fitur turunan, OOF training) | F1 tertinggi 0,643 pada threshold 0,387 | Untuk UAS, belum final |
| 8 | RF + class_weight (lampiran Pertemuan 5) | F1 0,294; Recall 0,179 | Hampir tidak membantu |
| 9 | PCA 90% + LR + class_weight (lampiran Pertemuan 6) | F1 0,481; Recall 0,726 | Tidak membantu |
| 10 | K-Means K = 2 (lampiran Pertemuan 6) | Silhouette 0,155 | Struktur lemah, analisis tambahan |

## Model card ringkas

| Bagian | Isi |
|---|---|
| Tujuan | Memprediksi karyawan yang berisiko resign dan menganalisis faktor yang berasosiasi dengannya, sebagai latihan metodologi machine learning |
| Data | IBM HR Analytics, 1.470 karyawan, 30 fitur setelah 4 kolom dibuang, target `Attrition` (16,12% Yes), data hipotetis |
| Metodologi | Split stratified 80:20, Stratified 5-Fold CV pada data training, preprocessing di dalam Pipeline, metrik utama F1 dan Recall kelas resign |
| Hasil awal | Logistic Regression F1 0,561 (Recall 0,442). Dengan class_weight, Recall 0,737 dan Precision 0,372. Random Forest dan Gradient Boosting overfitting (gap F1 0,679 dan 0,445). |
| Keterbatasan | Data kecil dan hipotetis, kasus resign sedikit, hiperparameter belum dituning, Precision rendah pada model dengan Recall tinggi |
| Penggunaan | Hanya untuk pembelajaran. Tidak untuk keputusan SDM terhadap individu: prediksi dapat keliru dan menunjukkan asosiasi, bukan sebab-akibat. |

## Rencana menuju UAS

Hyperparameter tuning (GridSearchCV atau RandomizedSearchCV), threshold tuning, SMOTE di dalam pipeline, feature importance dan SHAP, pemilihan model akhir berdasarkan bukti, lalu evaluasi satu kali di test set.

## Penggunaan AI

AI digunakan sebagai alat bantu penyusunan kerangka dan kode. Seluruh eksperimen dijalankan dan hasilnya diperiksa oleh anggota kelompok. [Sesuaikan dengan kenyataan.]
