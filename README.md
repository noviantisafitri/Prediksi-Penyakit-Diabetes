# Laporan Proyek Machine Learning - Novianti Safitri

## Domain Proyek

Diabetes adalah salah satu penyakit kronis paling umum di dunia dan dapat menimbulkan komplikasi serius jika tidak ditangani sejak dini. Berdasarkan data dari International Diabetes Federation (IDF), lebih dari 500 juta orang dewasa hidup dengan diabetes pada tahun 2021. Oleh karena itu, pendeteksian dini menjadi sangat penting. Dalam proyek ini, dibangun model machine learning untuk memprediksi kemungkinan seseorang mengidap diabetes berdasarkan data medis sederhana, sehingga dapat membantu dalam diagnosis awal dan pengambilan keputusan medis.

Referensi: [International Diabetes Federation](https://idf.org/)

## Business Understanding

### Problem Statements
- Bagaimana mengidentifikasi pasien berisiko diabetes berdasarkan parameter medis?
- Bagaimana meningkatkan performa prediksi diagnosis diabetes dengan model machine learning?

### Goals
- Mengembangkan model klasifikasi untuk memprediksi diabetes dari parameter medis pasien.
- Mengoptimalkan performa model menggunakan preprocessing, balancing data, PCA, dan hyperparameter tuning.

### Solution Statements
- Menggunakan algoritma Random Forest Classifier untuk membangun model prediktif.
- Menerapkan teknik SMOTE untuk mengatasi ketidakseimbangan kelas.
- Menggunakan PCA untuk reduksi dimensi dan meningkatkan efisiensi model.
- Melakukan hyperparameter tuning dengan GridSearchCV untuk mendapatkan performa terbaik.

## Data Understanding

Dataset yang digunakan adalah Pima Indian Diabetes Dataset yang tersedia di [GitHub](https://github.com/noviantisafitri/Prediksi-Penyakit-Diabetes/blob/main/diabetes.csv). Dataset terdiri dari 768 entri dan 9 kolom fitur medis.

### Variabel dalam dataset:
- Pregnancies: Jumlah kehamilan
- Glucose: Kadar glukosa darah
- BloodPressure: Tekanan darah diastolik (mm Hg)
- SkinThickness: Ketebalan lipatan kulit triceps (mm)
- Insulin: Tingkat insulin serum (mu U/ml)
- BMI: Indeks massa tubuh (kg/m²)
- DiabetesPedigreeFunction: Indeks riwayat diabetes keluarga
- Age: Usia pasien
- Outcome: Label target (0 = tidak diabetes, 1 = diabetes)

Hasil EDA menunjukkan tidak ada missing values secara eksplisit, namun nilai 0 pada fitur seperti Glucose, BloodPressure, Insulin, dan BMI diduga merepresentasikan data yang hilang. Korelasi tertinggi dengan Outcome terdapat pada Glucose (0.47), BMI (0.29), Age (0.24), dan Pregnancies (0.22), sedangkan fitur lainnya memiliki korelasi lemah.

## Data Preparation

Tahapan preprocessing:
1. **Normalisasi** fitur numerik menggunakan MinMaxScaler untuk menyamakan skala antar fitur.
2. **Balancing data** dengan SMOTE untuk mengatasi ketidakseimbangan kelas pada label Outcome.
3. **Reduksi dimensi** menggunakan PCA untuk mempertahankan 95% varian dengan fitur lebih sedikit.
4. **Split data** menjadi training dan testing (80:20) untuk evaluasi performa model.

## Modeling

Model utama yang digunakan adalah **Random Forest Classifier** karena kemampuannya menangani data tidak linier dan memberikan interpretasi terhadap fitur penting. Proses tuning parameter dilakukan dengan **GridSearchCV** pada kombinasi parameter:
- n_estimators: [100, 150]
- max_depth: [10, 15]
- min_samples_leaf: [3, 5]

Setelah proses training, model dengan parameter terbaik dipilih dan digunakan untuk evaluasi.

## Evaluation

Evaluasi dilakukan dengan metrik:
- **Accuracy**: proporsi prediksi benar dari seluruh prediksi
- **Precision**: seberapa tepat model dalam memprediksi kelas positif
- **Recall**: seberapa baik model menangkap semua kelas positif
- **F1 Score**: harmonisasi antara precision dan recall

Hasil evaluasi menunjukkan:
- Train Accuracy: tinggi, tanpa overfitting signifikan
- Test Accuracy: menunjukkan generalisasi model yang baik
- Classification Report: memberikan metrik evaluasi per kelas
- Confusion Matrix: memperlihatkan distribusi prediksi benar dan salah
- Feature Importance (setelah PCA): memberikan gambaran kontribusi masing-masing fitur terhadap prediksi

Model ini dapat menjadi alat bantu diagnosis awal diabetes berdasarkan input medis sederhana.
