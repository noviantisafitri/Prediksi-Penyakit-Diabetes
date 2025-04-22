# Laporan Proyek Machine Learning - Novianti Safitri

## Domain Proyek

Diabetes merupakan salah satu penyakit kronis yang dapat menyebabkan komplikasi serius jika tidak didiagnosis dan ditangani sejak dini. Berdasarkan data dari International Diabetes Federation (IDF), diperkirakan bahwa lebih dari 500 juta orang dewasa di dunia hidup dengan diabetes pada tahun 2021. Pendeteksian dini terhadap penyakit ini menjadi sangat penting untuk mencegah komplikasi jangka panjang.

Proyek ini bertujuan untuk membuat model machine learning yang dapat memprediksi kemungkinan seseorang menderita diabetes berdasarkan parameter medis yang tersedia. Dengan model ini, diharapkan proses deteksi awal dapat dilakukan lebih cepat dan akurat.

Referensi: [International Diabetes Federation](https://idf.org/)

## Business Understanding

### Problem Statements
- Bagaimana cara mengidentifikasi pasien yang berisiko tinggi menderita diabetes berdasarkan parameter medis?
- Bagaimana cara meningkatkan akurasi prediksi diagnosis diabetes menggunakan model machine learning?

### Goals
- Membangun model klasifikasi untuk memprediksi kemungkinan seseorang terkena diabetes.
- Mengoptimalkan performa model melalui teknik preprocessing, resampling, reduksi dimensi, dan tuning parameter.

### Solution statements
- Menggunakan algoritma Random Forest Classifier untuk membangun model prediksi.
- Menerapkan teknik SMOTE untuk menangani ketidakseimbangan kelas pada data.
- Menerapkan Principal Component Analysis (PCA) untuk reduksi dimensi.
- Melakukan hyperparameter tuning menggunakan GridSearchCV untuk meningkatkan performa model.

## Data Understanding

Dataset yang digunakan bersumber dari [GitHub Repository](https://github.com/noviantisafitri/Prediksi-Penyakit-Diabetes/blob/main/diabetes.csv) dan merupakan turunan dari Pima Indian Diabetes dataset. Dataset ini memiliki 8 fitur dan 1 label.

### Variabel-variabel pada dataset adalah sebagai berikut:
- Pregnancies: Jumlah kehamilan
- Glucose: Kadar glukosa dalam darah
- BloodPressure: Tekanan darah diastolik
- SkinThickness: Ketebalan lipatan kulit triceps
- Insulin: Tingkat insulin serum
- BMI: Indeks massa tubuh
- DiabetesPedigreeFunction: Riwayat diabetes dalam keluarga
- Age: Usia
- Outcome: Label (0 = tidak diabetes, 1 = diabetes)

Visualisasi awal dilakukan dengan:
- Matriks korelasi antar fitur
- Histogram distribusi fitur

## Data Preparation

Langkah-langkah yang dilakukan dalam tahap persiapan data:
1. Mengecek missing values dan duplikat.
2. Melakukan normalisasi fitur menggunakan MinMaxScaler.
3. Menyeimbangkan data menggunakan SMOTE untuk mengatasi ketimpangan jumlah antara kelas 0 dan 1.
4. Melakukan PCA untuk mengurangi dimensi fitur dengan mempertahankan 95% varians data.

## Modeling

Model yang digunakan adalah **Random Forest Classifier**. Alasan pemilihan model ini karena robust terhadap outlier dan dapat menangani data dengan fitur yang banyak.

Tuning parameter dilakukan menggunakan GridSearchCV dengan parameter sebagai berikut:
- n_estimators: [100, 150]
- max_depth: [10, 15]
- min_samples_leaf: [3, 5]

Model dilatih dengan data hasil PCA dan data telah diseimbangkan sebelumnya.

## Evaluation

Metrik evaluasi yang digunakan adalah:
- Accuracy
- Precision
- Recall
- F1-score

Hasil evaluasi model:
- **Train Accuracy**: tinggi (overfitting tidak signifikan)
- **Test Accuracy**: menunjukkan generalisasi model yang baik
- **Classification Report**: menunjukkan performa model dalam memprediksi masing-masing kelas
- **Confusion Matrix**: digunakan untuk melihat jumlah prediksi yang benar dan salah

Visualisasi tambahan:
- Heatmap confusion matrix
- Grafik feature importance setelah PCA

Dengan pendekatan ini, model mampu memberikan prediksi yang cukup akurat dan dapat digunakan untuk deteksi awal penyakit diabetes dengan input parameter medis yang sederhana.

---
