# Employee Attrition Prediction

## Project Information

- **Project ID:** W09
- **Nama Kelompok:** Employee Attrition
- **Anggota:** Martin Sormin

## Deskripsi Masalah

Employee attrition merupakan kondisi ketika karyawan meninggalkan perusahaan. Tingginya tingkat attrition dapat memengaruhi stabilitas tenaga kerja, produktivitas perusahaan, serta meningkatkan biaya perekrutan dan pelatihan karyawan baru.

Proyek ini menggunakan dataset **IBM HR Analytics Employee Attrition & Performance** untuk menganalisis karakteristik karyawan yang berkaitan dengan employee attrition dan membangun model Machine Learning untuk memprediksi apakah seorang karyawan berpotensi meninggalkan perusahaan.

Permasalahan dalam proyek ini difokuskan pada beberapa hal berikut:

1. Memahami karakteristik dan pola data karyawan.
2. Mengidentifikasi faktor atau fitur yang memiliki hubungan dengan employee attrition melalui Exploratory Data Analysis (EDA).
3. Melakukan preprocessing dan feature engineering untuk mempersiapkan data.
4. Membangun dan membandingkan beberapa model Machine Learning untuk memprediksi attrition.
5. Mengevaluasi performa model menggunakan metrik seperti **F1-score, Recall, Precision, dan ROC-AUC**.

Pada tahap awal, beberapa model yang digunakan antara lain:

- Logistic Regression
- Logistic Regression dengan `class_weight="balanced"`
- K-Nearest Neighbors (KNN)
- Decision Tree
- Random Forest
- Gradient Boosting

Berdasarkan hasil eksperimen awal, **Logistic Regression dengan fitur asli dan fitur turunan** dipilih sebagai kandidat utama karena memberikan performa yang baik dengan tingkat overfitting yang relatif rendah.

## Dataset

Dataset yang digunakan adalah **IBM HR Analytics Employee Attrition & Performance** dari Kaggle.

File dataset yang digunakan:

`WA_Fn-UseC_-HR-Employee-Attrition.csv`

Target yang diprediksi adalah kolom **Attrition**, dengan:

- `Yes` = karyawan meninggalkan perusahaan
- `No` = karyawan tetap bekerja

## Struktur Repository

```text
.
├── employee_attrition_milestone1_kelompok_09.ipynb
├── WA_Fn-UseC_-HR-Employee-Attrition.csv
└── README.md
```

## Petunjuk Penggunaan Repository

1. Clone repository ini ke komputer lokal.

```bash
git clone <URL_REPOSITORY>
```

2. Masuk ke direktori repository.

```bash
cd <NAMA_REPOSITORY>
```

3. Pastikan file dataset `WA_Fn-UseC_-HR-Employee-Attrition.csv` berada dalam direktori yang sesuai dengan notebook.

4. Install library Python yang diperlukan, seperti:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

5. Jalankan Jupyter Notebook:

```bash
jupyter notebook
```

6. Buka file:

```text
employee_attrition_milestone1_kelompok_09.ipynb
```

7. Jalankan notebook dari awal hingga akhir (**Run All**) untuk melakukan proses analisis data, preprocessing, feature engineering, pelatihan model, dan evaluasi awal.

## Catatan

- Notebook menggunakan `RANDOM_STATE = 42` untuk menjaga reproduksibilitas eksperimen.
- Data dibagi menggunakan metode **Stratified Hold-Out 80:20**.
- Validasi model dilakukan menggunakan **Stratified 5-Fold Cross-Validation**.
- Data testing disimpan untuk evaluasi akhir dan tidak digunakan dalam proses pemilihan model pada Milestone 1.
