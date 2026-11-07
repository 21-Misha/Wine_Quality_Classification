# Wine Quality Classification

## Deskripsi

Proyek ini membahas penerapan metode klasifikasi untuk memprediksi kualitas wine berdasarkan karakteristik fisikokimia yang terkandung di dalamnya.

Analisis dilakukan menggunakan Python dengan menerapkan dua algoritma klasifikasi, yaitu Decision Tree dan Random Forest. Kedua algoritma dibandingkan menggunakan metode 5-Fold Stratified Cross Validation untuk mengetahui model dengan performa terbaik.

Model terpilih kemudian digunakan untuk memprediksi dataset testing. Proses prediksi dilakukan menggunakan lima model hasil Cross Validation, kemudian hasil akhirnya ditentukan melalui metode Majority Voting.

## Tujuan Analisis

- Mengidentifikasi karakteristik dan distribusi data kualitas wine.
- Melakukan pembersihan dan persiapan data sebelum pemodelan.
- Membangun model klasifikasi menggunakan Decision Tree dan Random Forest.
- Membandingkan performa kedua algoritma menggunakan 5-Fold Cross Validation.
- Menentukan model dengan performa terbaik berdasarkan rata-rata akurasi.
- Melakukan prediksi kualitas wine menggunakan metode Majority Voting.

## Dataset

Dataset yang digunakan terdiri dari tiga file:

| Nama File | Jumlah Data | Keterangan |
|---|---:|---|
| data_training.csv | 857 | Data untuk pelatihan dan evaluasi model |
| data_testing.csv | 286 | Data untuk prediksi |
| hasilprediksi_3digitNIMterakhir.csv | 286 | Template hasil prediksi |

Terdapat 11 variabel yang digunakan sebagai fitur prediktor:

1. Fixed Acidity
2. Volatile Acidity
3. Citric Acid
4. Residual Sugar
5. Chlorides
6. Free Sulfur Dioxide
7. Total Sulfur Dioxide
8. Density
9. pH
10. Sulphates
11. Alcohol

Variabel target yang digunakan adalah `quality`, sedangkan `Id` hanya berfungsi sebagai identitas setiap data dan tidak digunakan dalam pemodelan.

## Metodologi

### 1. Persiapan Data

Tahap awal dilakukan dengan membaca ketiga dataset, memeriksa struktur data, melihat statistik deskriptif, serta mengamati distribusi kategori kualitas wine.

### 2. Pembersihan Data

Tahap ini meliputi pemeriksaan missing values, pemeriksaan data duplikat, serta pemisahan variabel prediktor dan target.

Penanganan missing values disiapkan menggunakan imputasi median. Normalisasi tidak diterapkan karena algoritma Decision Tree dan Random Forest tidak memerlukan feature scaling.

### 3. Pembuatan Model

Dua algoritma klasifikasi digunakan dalam analisis ini:

**Decision Tree**

Algoritma klasifikasi yang menggunakan struktur pohon keputusan untuk menentukan kategori berdasarkan kondisi pada setiap fitur.

**Random Forest**

Algoritma ensemble yang menggabungkan beberapa pohon keputusan untuk menghasilkan prediksi berdasarkan voting mayoritas.

Kedua algoritma dibandingkan menggunakan metode **5-Fold Stratified Cross Validation**. Dataset training dibagi menjadi lima bagian dengan proporsi kelas yang tetap terjaga.

Setiap model diuji sebanyak lima kali menggunakan kombinasi data training dan validasi yang berbeda. Nilai akurasi dari setiap fold kemudian dihitung rata-ratanya untuk menentukan model terbaik.

### 4. Evaluasi Model

Evaluasi dilakukan menggunakan beberapa metrik klasifikasi:

- **Accuracy:** Mengukur proporsi prediksi yang benar.
- **Precision:** Mengukur ketepatan prediksi pada setiap kelas.
- **Recall:** Mengukur kemampuan model mengenali data pada setiap kelas.
- **F1-Score:** Mengukur keseimbangan antara precision dan recall.
- **Confusion Matrix:** Menampilkan perbandingan antara kelas aktual dan hasil prediksi.

Selain itu, rata-rata akurasi dan standar deviasi digunakan untuk membandingkan performa kedua algoritma.

### 5. Prediksi Data Testing

Model terbaik yang diperoleh dari proses Cross Validation digunakan untuk membangun lima model berdasarkan pembagian data pada masing-masing fold.

Kelima model tersebut kemudian digunakan untuk memprediksi 286 data testing. Hasil prediksi dari setiap model digabungkan menggunakan metode **Majority Voting**, yaitu menentukan kategori quality berdasarkan suara terbanyak.

Hasil akhir kemudian dimasukkan ke dalam template yang telah disediakan dan disimpan dalam format CSV.

## Hasil Analisis

Hasil dari proses klasifikasi berupa:

1. Perbandingan performa Decision Tree dan Random Forest berdasarkan 5-Fold Cross Validation.
2. Evaluasi model menggunakan accuracy, precision, recall, F1-score, dan confusion matrix.
3. Model klasifikasi terbaik yang disimpan dalam format `.pkl`.
4. Hasil prediksi kualitas wine pada 286 data testing.

## Tools dan Library

Proyek ini menggunakan beberapa tools dan library berikut:

- Python
- Google Colab
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Joblib
- SciPy

## Output

| Nama File | Keterangan |
|---|---|
| model_wine_quality_5fold.pkl | Menyimpan lima model hasil Cross Validation |
| hasil_prediksi.csv | Hasil akhir prediksi kualitas wine |

File `hasil_prediksi.csv` terdiri dari dua kolom, yaitu `Id` dan `Quality`, dengan total 286 data.

## Struktur Repository

```text
Wine-Quality-Classification/
│
├── dataset/
│   ├── data_training.csv
│   ├── data_testing.csv
│   └── hasilprediksi_3digitNIMterakhir.csv
│
├── notebook/
│   └── UTS_Wine_Quality_Classification.ipynb
│
├── output/
│   ├── model_wine_quality_5fold.pkl
│   └── hasil_prediksi.csv
│
└── README.md
```

## Kesimpulan

Analisis ini menerapkan algoritma Decision Tree dan Random Forest untuk mengklasifikasikan kualitas wine berdasarkan karakteristik fisikokimianya.

Penggunaan 5-Fold Cross Validation membantu membandingkan performa kedua algoritma melalui beberapa pembagian data. Model dengan rata-rata akurasi tertinggi kemudian digunakan untuk melakukan prediksi pada dataset testing.

Penerapan Majority Voting digunakan untuk menggabungkan hasil prediksi dari lima model sehingga diperoleh kategori kualitas wine sebagai hasil akhir klasifikasi.
