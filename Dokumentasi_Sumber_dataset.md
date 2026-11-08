# Dokumentasi Sumber Dataset

## 1. Identitas Dataset

Dataset yang digunakan dalam proyek ini adalah **IBM HR Analytics Employee Attrition & Performance**.

Dataset ini diperoleh melalui platform Kaggle dan digunakan untuk keperluan analisis serta pengembangan model Machine Learning.

**Informasi Dataset:**

- **Nama Dataset:** IBM HR Analytics Employee Attrition & Performance
- **Platform:** Kaggle
- **Pengunggah:** Pavan Subhasht
- **Format:** CSV
- **Nama File:** `WA_Fn-UseC_-HR-Employee-Attrition.csv`
- **Jumlah Data:** 1.470 baris
- **Jumlah Atribut:** 35 kolom
- **Jenis Permasalahan:** Klasifikasi Biner
- **Variabel Target:** `Attrition`

---

## 2. Deskripsi Dataset

IBM HR Analytics Employee Attrition & Performance merupakan dataset yang berisi informasi mengenai karakteristik karyawan dan kondisi pekerjaan.

Beberapa informasi yang terdapat dalam dataset meliputi:

- Usia karyawan (*Age*).
- Departemen (*Department*).
- Jabatan (*JobRole*).
- Pendapatan bulanan (*MonthlyIncome*).
- Kepuasan kerja (*JobSatisfaction*).
- Pengalaman kerja (*YearsAtCompany*).
- Status karyawan (*Attrition*).

Dataset ini merupakan data fiktif untuk keperluan analisis dan pembelajaran, bukan catatan aktual karyawan IBM.

---

## 3. Tujuan Penggunaan Dataset

Dataset ini digunakan untuk menganalisis faktor-faktor yang berkaitan dengan keluarnya karyawan dari perusahaan (*Employee Attrition*).

Variabel `Attrition` digunakan sebagai target dalam proses pengembangan model Machine Learning.

Terdapat dua kategori pada variabel target:

- **Yes:** Karyawan meninggalkan perusahaan.
- **No:** Karyawan tetap bekerja di perusahaan.

Model Machine Learning dikembangkan untuk mempelajari pola data dan memprediksi status attrition karyawan.

---

## 4. Sumber Dataset

Dataset dapat diperoleh melalui platform Kaggle pada tautan berikut:

**IBM HR Analytics Employee Attrition & Performance**

[Klik di sini untuk membuka dataset di Kaggle](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset)

---

## 5. Cara Memperoleh Dataset

1. Buka tautan dataset Kaggle di atas.
2. Login menggunakan akun Kaggle atau buat akun baru.
3. Buka halaman dataset IBM HR Analytics Employee Attrition & Performance.
4. Unduh dataset dalam format CSV.
5. Pastikan nama file sesuai dengan `WA_Fn-UseC_-HR-Employee-Attrition.csv`.
6. Letakkan file CSV di folder yang sama dengan notebook atau unggah ke Google Colab.

> **Catatan:** Dataset tidak disertakan langsung dalam repositori GitHub ini. Pengguna perlu mengunduh dataset secara mandiri melalui tautan Kaggle.

---

## 6. Kode Membaca Dataset

Berikut kode Python yang digunakan untuk membaca dataset menggunakan library Pandas.

```python
import pandas as pd

# Membaca dataset
file_path = "WA_Fn-UseC_-HR-Employee-Attrition.csv"
df = pd.read_csv(file_path)

# Menampilkan ukuran dataset
print("Jumlah baris dan kolom:", df.shape)

# Menampilkan lima data pertama
display(df.head())

# Menampilkan informasi dataset
df.info()

# Memeriksa jumlah data kosong
print("Jumlah data kosong:", df.isnull().sum().sum())

# Menampilkan distribusi target
print("\nDistribusi Attrition:")
print(df["Attrition"].value_counts())
```

---

## 7. Keterangan Penggunaan

Dataset ini digunakan sebagai bahan penelitian dan pembelajaran dalam penerapan algoritma Machine Learning, khususnya untuk permasalahan klasifikasi biner.

Tahapan pengolahan data meliputi eksplorasi data, preprocessing, pelatihan model, dan evaluasi performa model.
