# Laporan Proyek Machine Learning - Novianti Safitri

## Domain Proyek

Diabetes merupakan salah satu penyakit kronis yang mengalami peningkatan signifikan dari tahun ke tahun. Menurut World Health Organization (2024), jumlah penderita diabetes meningkat dari 200 juta pada tahun 1990 menjadi 830 juta pada tahun 2022, dengan prevalensi yang meningkat lebih cepat di negara-negara berpenghasilan rendah dan menengah dibandingkan negara-negara berpenghasilan tinggi. Diabetes tidak hanya berdampak pada kualitas hidup individu, tetapi juga menyebabkan berbagai komplikasi serius seperti kebutaan, gagal ginjal, serangan jantung, stroke, hingga amputasi anggota tubuh. Pada tahun 2021, diabetes dan penyakit ginjal akibat diabetes menyebabkan lebih dari 2 juta kematian di seluruh dunia, dan sekitar 11% kematian akibat penyakit kardiovaskular disebabkan oleh kadar gula darah yang tinggi (World Health Organization, 2024).

Di Amerika Serikat, diabetes telah menjadi masalah kesehatan yang sangat serius. Pada tahun 2021, terdapat sekitar 38,4 juta orang Amerika yang hidup dengan diabetes, yang mencakup 11,6% dari total populasi, termasuk 2 juta penderita diabetes tipe 1 (American Diabetes Association, 2023). Prevalensi diabetes pada lansia (usia ≥65 tahun) sangat tinggi, yakni sebesar 29,2%. Tidak hanya itu, sebanyak 97,6 juta orang dewasa Amerika diketahui mengalami prediabetes, suatu kondisi yang meningkatkan risiko terkena diabetes tipe 2 dan berbagai komplikasi kesehatan lainnya (Centers for Disease Control and Prevention, 2024). Prediabetes sendiri dapat dikendalikan dengan perubahan gaya hidup, yang terbukti dapat mengurangi risiko berkembangnya diabetes tipe 2 hingga setengahnya.

Masalah lain yang menonjol adalah masih rendahnya tingkat pengobatan diabetes, khususnya di negara-negara berpenghasilan rendah dan menengah, di mana lebih dari setengah penderita tidak menjalani pengobatan yang semestinya (World Health Organization, 2024). Selain beban kesehatan, diabetes juga menimbulkan beban ekonomi yang besar. Di Amerika Serikat, total biaya yang dihabiskan untuk diabetes pada tahun 2022 mencapai $412,9 miliar, terdiri dari $306,6 miliar untuk biaya medis langsung dan $106,3 miliar untuk biaya tidak langsung (American Diabetes Association, 2023).

Melihat tingginya prevalensi dan dampak luas dari diabetes, baik dari segi kesehatan maupun ekonomi, maka dibutuhkan upaya preventif dan deteksi dini melalui pendekatan teknologi, seperti penerapan machine learning untuk prediksi penyakit diabetes. Dengan memanfaatkan data kesehatan dan algoritma pembelajaran mesin, prediksi dini terhadap risiko diabetes dapat membantu tenaga medis dan masyarakat dalam mengambil langkah intervensi lebih awal untuk mencegah komplikasi yang lebih serius di masa depan.

Referensi tambahan:
1. World Health Organization. (2024). Diabetes. Retrieved from https://www.who.int/news-room/fact-sheets/detail/diabetes
2. Centers for Disease Control and Prevention. (2024). Prediabetes - Your Chance to Prevent Type 2 Diabetes. Retrieved from https://www.cdc.gov/diabetes/prevention-type-2/prediabetes-prevent-type-2.html
3. American Diabetes Association. (2023). Statistics About Diabetes. Retrieved from https://diabetes.org/about-diabetes/statistics/about-diabetes

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

Model utama yang digunakan adalah **Random Forest Classifier** karena kemampuannya menangani data tidak linier, tahan terhadap overfitting (terutama dengan cukup banyak data dan tuning parameter yang tepat), serta mampu memberikan interpretasi terhadap pentingnya fitur. Proses tuning parameter dilakukan dengan GridSearchCV pada kombinasi parameter berikut:
- n_estimators: [100, 150]
- max_depth: [10, 15]
- min_samples_leaf: [3, 5]

Setelah proses pelatihan, model dengan parameter terbaik dipilih dan digunakan untuk evaluasi. Random Forest Classifier dipilih sebagai model utama karena memiliki beberapa kelebihan, di antaranya mampu menangani data berdimensi tinggi serta fitur yang saling berinteraksi secara kompleks. Selain itu, model ini juga memberikan estimasi feature importance yang berguna untuk interpretasi dan memiliki performa yang stabil dan akurat, bahkan saat diterapkan pada data yang tidak terdistribusi secara linier. Meskipun demikian, Random Forest juga memiliki beberapa kekurangan, seperti sifatnya yang black box, sehingga interpretasi terhadap keputusan prediksi individu menjadi lebih sulit dibandingkan dengan model linier atau pohon keputusan tunggal. Selain itu, model juga rentan terhadap overfitting apabila tuning parameter tidak dilakukan secara tepat, khususnya pada dataset yang berukuran kecil.

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
