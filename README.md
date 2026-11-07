# Wine Quality Classification

## Deskripsi

Proyek ini membahas penerapan metode klasifikasi untuk memprediksi kualitas wine berdasarkan karakteristik fisikokimia yang terkandung di dalamnya.

Analisis dilakukan menggunakan Python dengan menerapkan dua algoritma klasifikasi, yaitu Decision Tree dan Random Forest. Performa kedua algoritma dibandingkan menggunakan metode 5-Fold Stratified Cross Validation untuk menentukan model dengan hasil terbaik.

Berdasarkan hasil pengujian, Random Forest memperoleh performa terbaik dengan rata-rata akurasi sebesar 64,65%. Model tersebut kemudian digunakan untuk memprediksi data testing menggunakan lima model hasil Cross Validation yang digabungkan melalui metode Majority Voting.

## Tujuan Analisis

- Mengidentifikasi karakteristik dan distribusi data kualitas wine.
- Melakukan pemeriksaan dan persiapan data sebelum pemodelan.
- Membangun model klasifikasi menggunakan Decision Tree dan Random Forest.
- Membandingkan performa kedua algoritma menggunakan 5-Fold Cross Validation.
- Menentukan model terbaik berdasarkan rata-rata akurasi.
- Memprediksi kualitas wine pada data testing menggunakan Majority Voting.

## Dataset

Dataset yang digunakan terdiri dari tiga file:

| Nama File | Jumlah Data | Keterangan |
|---|---:|---|
| `data_training.csv` | 857 | Data untuk pelatihan dan evaluasi model |
| `data_testing.csv` | 286 | Data untuk prediksi |
| `hasilprediksi_3digitNIMterakhir.csv` | 286 | Template hasil prediksi |

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

Variabel target yang digunakan adalah `quality`, sedangkan `Id` hanya berfungsi sebagai identitas data dan tidak digunakan dalam pemodelan.

## Metodologi

### 1. Persiapan Data

Tahap awal dilakukan dengan membaca dataset training, testing, dan template hasil prediksi. Selanjutnya, dilakukan pemeriksaan struktur data, tipe data, statistik deskriptif, serta distribusi kategori kualitas wine.

### 2. Pemeriksaan dan Pembersihan Data

Pemeriksaan dilakukan terhadap missing values dan data duplikat pada dataset training maupun testing.

Penanganan missing values disiapkan menggunakan metode imputasi median melalui Pipeline. Selain itu, kolom `Id` dipisahkan dari fitur prediktor karena hanya berfungsi sebagai identitas data.

Normalisasi atau feature scaling tidak diterapkan karena algoritma Decision Tree dan Random Forest tidak memerlukannya.

### 3. Pembuatan Model

Dua algoritma klasifikasi digunakan dalam analisis ini:

**Decision Tree**

Algoritma klasifikasi yang menggunakan struktur pohon keputusan untuk menentukan kategori berdasarkan kondisi pada setiap fitur.

**Random Forest**

Algoritma ensemble yang menggabungkan beberapa pohon keputusan untuk menghasilkan prediksi berdasarkan voting.

Pada Random Forest digunakan 300 pohon keputusan (`n_estimators=300`). Kedua algoritma menggunakan `class_weight='balanced'` untuk membantu menangani distribusi kelas yang tidak seimbang.

Pengujian dilakukan menggunakan **5-Fold Stratified Cross Validation**. Dataset training dibagi menjadi lima bagian dengan proporsi kelas yang tetap terjaga. Setiap model dilatih dan divalidasi secara bergantian pada lima pembagian data tersebut.

### 4. Evaluasi dan Pemilihan Model

Performa kedua algoritma dibandingkan berdasarkan rata-rata akurasi dan standar deviasi dari lima fold.

Model dengan rata-rata akurasi tertinggi dipilih sebagai model terbaik. Selanjutnya, model terpilih dievaluasi menggunakan:

- **Accuracy:** Mengukur proporsi prediksi yang benar.
- **Precision:** Mengukur ketepatan prediksi pada setiap kelas.
- **Recall:** Mengukur kemampuan model mengenali data pada setiap kelas.
- **F1-Score:** Mengukur keseimbangan antara precision dan recall.
- **Confusion Matrix:** Menampilkan perbandingan antara kelas aktual dan hasil prediksi.

### 5. Prediksi Data Testing

Model terbaik digunakan untuk membangun lima model berdasarkan pembagian data pada masing-masing fold. Setiap model kemudian digunakan untuk memprediksi 286 data testing.

Hasil prediksi dari kelima model digabungkan menggunakan metode **Majority Voting**, yaitu menentukan kategori quality berdasarkan suara terbanyak.

Hasil akhir dimasukkan ke dalam template yang telah disediakan dan disimpan dalam format CSV.

## Hasil Analisis

### 1. Perbandingan Model

Berdasarkan hasil 5-Fold Stratified Cross Validation, diperoleh model terbaik sebagai berikut:

| Parameter | Hasil |
|---|---:|
| Model Terbaik | Random Forest |
| Rata-rata Akurasi | 0,6465 (64,65%) |
| Standar Deviasi | 0,0299 (2,99%) |

Hasil tersebut menunjukkan bahwa Random Forest memiliki rata-rata akurasi tertinggi dibandingkan Decision Tree.

### 2. Evaluasi Model Terbaik

Evaluasi lanjutan dilakukan menggunakan `cross_val_predict` untuk menghasilkan prediksi pada seluruh 857 data training melalui skema cross-validation.

Hasil evaluasi menunjukkan:

- Jumlah data training: 857.
- Jumlah prediksi benar: 554.
- Akurasi: 64,64%.
- Model lebih baik dalam mengklasifikasikan wine pada kategori quality 5 dan 6.
- Kesalahan klasifikasi masih ditemukan, terutama antara kategori quality 5 dan 6.

### 3. Prediksi Data Testing

Prediksi dilakukan terhadap 286 data testing menggunakan lima model Random Forest hasil Cross Validation. Hasil dari setiap model digabungkan menggunakan Majority Voting untuk memperoleh satu kategori kualitas akhir pada setiap data.

Hasil prediksi kemudian dimasukkan ke dalam template dan disimpan sebagai `hasil_prediksi.csv`.

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
| `model_wine_quality.pkl` | Model Random Forest yang dilatih menggunakan seluruh data training |
| `model_wine_quality_5fold.pkl` | Menyimpan lima model hasil Cross Validation |
| `hasil_prediksi.csv` | Hasil akhir prediksi kualitas wine pada 286 data testing |

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
│   └── Wine_Quality_Classification.ipynb
│
├── output/
│   ├── model_wine_quality.pkl
│   ├── model_wine_quality_5fold.pkl
│   └── hasil_prediksi.csv
│
└── README.md
```

## Kesimpulan

Berdasarkan hasil analisis, Random Forest merupakan model terbaik dibandingkan Decision Tree dalam mengklasifikasikan kualitas wine. Model Random Forest memperoleh rata-rata akurasi sebesar 64,65% dengan standar deviasi 2,99% berdasarkan pengujian menggunakan 5-Fold Stratified Cross Validation.

Pada evaluasi lanjutan menggunakan `cross_val_predict`, model memperoleh akurasi sebesar 64,64%, dengan 554 dari 857 data berhasil diklasifikasikan secara tepat. Model menunjukkan kemampuan yang lebih baik dalam mengenali wine dengan kategori quality 5 dan 6, meskipun masih terdapat kesalahan klasifikasi pada beberapa kategori.

Selanjutnya, lima model Random Forest hasil Cross Validation digunakan untuk memprediksi 286 data testing. Hasil prediksi dari kelima model digabungkan menggunakan Majority Voting untuk memperoleh hasil klasifikasi akhir.
