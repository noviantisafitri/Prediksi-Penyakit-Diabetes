# Laporan Proyek Machine Learning - Novianti Safitri

## Domain Proyek

Diabetes adalah salah satu penyakit kronis yang paling banyak diderita secara global dan dapat menimbulkan komplikasi serius seperti gagal ginjal, kebutaan, dan penyakit jantung. Menurut World Health Organization (2023), jumlah penderita diabetes meningkat secara signifikan setiap tahunnya dan diperkirakan menjadi penyebab kematian ke-7 di dunia pada tahun 2030. Selain itu, laporan dari Centers for Disease Control and Prevention (2022) menyebutkan bahwa 1 dari 3 orang dewasa di Amerika Serikat mengalami prediabetes, dan sebagian besar tidak menyadarinya. Dalam konteks ini, deteksi dini menjadi sangat krusial. Dengan memanfaatkan machine learning, kita dapat membangun sistem prediktif berbasis data medis sederhana untuk membantu diagnosis awal dan pengambilan keputusan klinis secara lebih efisien.

Referensi tambahan:
1. World Health Organization. (2023). Diabetes. https://www.who.int/news-room/fact-sheets/detail/diabetes
2. Centers for Disease Control and Prevention. (2022). Prediabetes - Your Chance to Prevent Type 2 Diabetes. https://www.cdc.gov/diabetes/basics/prediabetes.html
3. American Diabetes Association. (2023). Statistics About Diabetes. https://diabetes.org/about-diabetes/statistics


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

Dataset yang digunakan adalah Pima Indian Diabetes Dataset yang tersedia di [Kaggle](https://www.kaggle.com/datasets/akshaydattatraykhare/diabetes-dataset). Dataset terdiri dari 768 entri dan 9 kolom fitur medis.

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
