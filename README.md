# Laporan Proyek Machine Learning - Muhammad Hadi

---

### Project Overview

sistem rekomendasi film adalah cara paling keren untuk mendeskripsikan sebuah proses yang mencoba untuk memprediksi film yang mungkin disukai berdasarkan riwayat atau seseorang yang memiliki kemiripan.

singkatnya, sistem rekomendasi adalah sebuah alat yang didesain untuk memprediksi atau menyaring item berdasarkan perilaku pengguna.

sistem rekomendasi memiliki banyak keuntunguan, baik dari sisi pengguna maupun perusahaan. bagi pengguna, dengan adanya sistem rekomendasi, kebutuhan pengguna bisa dilayani secepat dan seakurat mungkin. sedangkan dari sisi perusahaan, mereka bisa membuat pengguna bertahan lama di platform mereka sehingga dapat menghasilkan keuntungan semaksimal mungkin. dengan adanya sistem rekomendasi yang bagus, hal ini tentunya juga akan memberikan masukan positif dari pengguna.

# Business Understanding

---

### Problem Statement

Berdasarkan latar belakang di atas, berikut ini batasan masalah yang dapat diselesaikan dengan proyek ini :

- Bagaimana cara merekomendasikan film yang dipersonalisasi untuk pengguna?

### Goals

- Membuat sistem rekomendasi film yang dipersonalisasi untuk pengguna.

### Solution Statement

Solusi yang dapat dilakukan adalah dengan membuat 2 algoritma Machine Learning sistem rekomendasi:

- **Content Based Filtering** Adalah rekomendasi berbasis konten yang merekomendasikan item yang memiliki kemiripan dengan item yang disukai/diinput pengguna sebelumnya.
- **Collaborative Filtering** merupakan metode yang digunakan untuk merekomendasikan item berdasarkan penilaian pengguna sebelumnya, dimana atribut yang digunakan bukan konten tetapi user behaviour. Contohnya yaitu merekomendasikan suatu item berdasarkan dari riwayat rating dari user tersebut maupun user lain

---

# Data Understanding

![cover image](https://raw.githubusercontent.com/hadiselamethariyanto/red-wine-quality-machine-learning/main/images/dataset-cover.jpg)
Gambar 1

Dataset yang digunakan dalam proyek ini merupakan sample data uji fisiokimia dari Portugal utara. Dataset ini bisa didapatkan di [Kaggle: Red Wine Quality](https://www.kaggle.com/datasets/uciml/red-wine-quality-cortez-et-al-2009).

**Berikut informasi pada dataset:**

- Dataset memiliki format CSV
- Dataset memiliki 1.599 sample dengan 12 fitur
- Dataset memiliki 1 fitur Integer dan 11 fitur decimal

**Variable – variable pada dataset**

- Alcohol: jumlah alcohol didalam wine
- Volatile acidity: adalah asam asetat tinggi dalam anggur yang menyebabkan rasa cuka yang tidak enak
- Sulphates: aditif anggur yang berkontribusi pada kadar SO2 dan bertindak sebagai antimikroba dan antioksidan
- Citric acid: bertindak sebagai pengawet untuk meningkatkan keasaman (jumlah kecil menambah kesegaran dan rasa anggur)
- Total sulfur dioxide: adalah jumlah SO2 bentuk bebas + terikat
- Density: anggur yang lebih manis memiliki kepadatan yang lebih tinggi
- Chlorides: jumlah garam dalam anggur
- Fixed Acidity: adalah asam non-volatil yang tidak mudah menguap
- pH: tingkat keasaman
- Free Sulfur Dioxide: itu mencegah pertumbuhan mikroba dan oksidasi anggur
- Residual sugar: adalah jumlah gula yang tersisa setelah fermentasi berhenti. Kuncinya adalah memiliki keseimbangan yang sempurna antara — manis dan asam (anggur > 45g/ltr manis)
- quality: ukuran kualitas untuk anggur merah, semakin besar angka semakin bagus kualitas anggur merah

### visualisasi boxplot outliers

![alcohol](https://raw.githubusercontent.com/hadiselamethariyanto/red-wine-quality-machine-learning/main/images/alcohol.png)
Gambar 2

pada gambar 2 dapat dilihat bahwa boxplot **alcohol** terdapat indikasi outliers

![sulphates](https://raw.githubusercontent.com/hadiselamethariyanto/red-wine-quality-machine-learning/main/images/sulphates.png)
Gambar 3

pada Gambar 3 dapat dilihat bahwa boxplot **sulphates** terdapat indikasi outliers.

![ph](https://raw.githubusercontent.com/hadiselamethariyanto/red-wine-quality-machine-learning/main/images/ph.png)
Gambar 4
pada Gambar 4 dapat dilihat bahwa boxplot **pH** terdapat indikasi outliers.

![fixed acidity](https://raw.githubusercontent.com/hadiselamethariyanto/red-wine-quality-machine-learning/main/images/fixed%20acidity.png)
Gambar 5
pada Gambar 5 dapat dilihat bahwa boxplot **fixed acidity** terdapat indikasi outliers.

![volatile acidity](https://raw.githubusercontent.com/hadiselamethariyanto/red-wine-quality-machine-learning/main/images/volatile%20acidity.png)
Gambar 6
pada Gambar 6 dapat dilihat bahwa boxplot **volatile acidity** terdapat indikasi outliers.

![citric acid](https://raw.githubusercontent.com/hadiselamethariyanto/red-wine-quality-machine-learning/main/images/citric%20acid.png)
Gambar 7
pada Gambar 7 dapat dilihat bahwa boxplot **citric acid** terdapat indikasi outliers.

![residual sugar](https://raw.githubusercontent.com/hadiselamethariyanto/red-wine-quality-machine-learning/main/images/residual%20sugar.png)
Gambar 8
pada Gambar 8 dapat dilihat bahwa boxplot **residual sugar** terdapat indikasi outliers.

![chlorides](https://raw.githubusercontent.com/hadiselamethariyanto/red-wine-quality-machine-learning/main/images/chlorides.png)
Gambar 9
pada Gambar 9 dapat dilihat bahwa boxplot **chlorieds** terdapat indikasi outliers.

![free sulfur dioxide](https://raw.githubusercontent.com/hadiselamethariyanto/red-wine-quality-machine-learning/main/images/free%20sulfur%20dioxide.png)
Gambar 10
pada Gambar 10 dapat dilihat bahwa boxplot **free sulfur dioxide** terdapat indikasi outliers.

![total sulfur dioxide](https://raw.githubusercontent.com/hadiselamethariyanto/red-wine-quality-machine-learning/main/images/total%20sulfur%20dioxide.png)
Gambar 11
pada Gambar 11 dapat dilihat bahwa boxplot **total sulfure dioxide** terdapat indikasi outliers.

![density](https://raw.githubusercontent.com/hadiselamethariyanto/red-wine-quality-machine-learning/main/images/density.png)
Gambar 12
pada Gambar 12 dapat dilihat bahwa boxplot **density** terdapat indikasi outliers.

![quality](https://raw.githubusercontent.com/hadiselamethariyanto/red-wine-quality-machine-learning/main/images/quality.png)
Gambar 13
pada Gambar 13 dapat dilihat bahwa boxplot **quality** terdapat indikasi outliers.

**Penanganan Outliers**

Pada proyek ini , hampir seluruh variable memiliki outliers, untuk menangani outliers, teknik IQR method bisa digunakan. IQR adalah singkatan dari Interquartile Range. untuk memahami apa itu IQR, ingatlah konsep kuartil. Kuartil dari suatu populasi adalah tiga nilai yang membagi distribusi data menjadi empat sebaran. Seperempat dari data berada di bawah kuartil pertama (Q1), setengah dari data berada di bawah kuartil kedua (Q2), dan tiga perempat dari data berada di kuartil ketiga (Q3). Dengan demikian interquartile range atau IQR = Q3 - Q1, untuk lebih jelasnya dapat diperhatikan pada bagian potongan code dibawah ini :

Pada proyek ini digunakan IQR method untuk menangani outliers yang pertama definisikan dulu outliers pada Q1 atau batas bawah yaitu 0.25 lalu outliers pada Q3 atau batas atas yaitu 0.75 kemudian hasil Q3 akan dikurangi dengan hasil Q1 setelah itu buat variabel baru yaitu wine untuk menampung hasil batas bawah dari pengurangan Q1 dengan 1,5 _ IQR. lalu untuk hasil batas atas digunakan penambahan 1.5 _ IQR dengan Q3

dan jika dibuat persamaan dapat dilihat sebagai berikut :

---

_Batas bawah = Q1 - 1.5 \* IQR_

_Batas atas = Q3 + 1.5 \* IQR_

---

setelah itu untuk melihat ukuran hasil penanganan _outliers_, variabel _wine_ dapat dipanggil dengan **wine.shape**. hasil penanganan outliers menghasilkan data baru yaitu **(1179, 12)**

### Univariate Analysis

Univariate Analysis adalah menganalisis setiap fitur secara terpisah.

Karena pada dataset tidak ada data kategorik, maka kita langsung menganalisis sebaran pada setiap fitur numerik dengan melihat histogram masing-masing fiturnya.

![univarate image](https://raw.githubusercontent.com/hadiselamethariyanto/red-wine-quality-machine-learning/main/images/univariete.png)
Gambar 14

Mari kita lihat histogram diatas, khususnya variable ‘quality’ yang menjadi target pada data kita.

- Rata-rata kualitas wine berada di angka 5 dan 6
- Bisa dilihat pH level anggur merah selalu berada di angka 3-3.8

### Multivariate Analysis

Multivariate Analysis menunjukkan hubungan antara dua atau lebih fitur dalam data.

**Analisis Fitur Numerik**

![multivariate image](https://raw.githubusercontent.com/hadiselamethariyanto/red-wine-quality-machine-learning/main/images/multivariate.png)
Gambar 15

Dari pola sebaran data(titik-titik) pada gambar diatas, kita bisa melihat adanya 3 pola yang terbentuk, yaitu positive, negative dan pola acak yang artinya tidak memiliki korelasi apapun.

Untuk pola positif, kita bisa melihat hubungan yang positif antara critical acid, alcohol dan sulphates. Meskipun anggur merah dengan kandungan alcohol yang lebih tinggi kurang popular, akan tetapi mereka memiliki kualitas yang bagus.

Untuk pola negative, variable volatile acidity, density, total sulfur dioxide dan cholireds memiliki pola negative dengan kualitas. Ini sangat masuk akal karena anggur merah yang kurang manis dan tingkat keasaman yang lebih rendah lebih disukai dalam pengujian kualitas.

Untuk pola acak, residual sugar, pH, dan free sulfur dioxide tidak memiliki kolerasi apapun dengan kualitas.

Agar lebih jelas, mari kita lihat skor korelasi pada gambar dibawah ini.

![korelasi image](https://raw.githubusercontent.com/hadiselamethariyanto/red-wine-quality-machine-learning/main/images/korelasi.png)
Gambar 16

Karena skor residual sugar, pH, dan free sulfur dioxide sangat kecil, maka fitur tersebut kita drop.

|     | fixed acidity | volatile acidity | citric acid | chlorides | total sulfur dioxide | density | sulphates | alcohol | quality |
| --- | ------------- | ---------------- | ----------- | --------- | -------------------- | ------- | --------- | ------- | ------- |
| 0   | 7.4           | 0.70             | 0.00        | 0.076     | 34.0                 | 0.9978  | 0.56      | 9.4     | 5       |
| 1   | 7.8           | 0.88             | 0.00        | 0.098     | 67.0                 | 0.9968  | 0.68      | 9.8     | 5       |
| 2   | 7.8           | 0.76             | 0.04        | 0.092     | 54.0                 | 0.9970  | 0.65      | 9.8     | 5       |
| 3   | 11.2          | 0.28             | 0.56        | 0.075     | 60.0                 | 0.9980  | 0.58      | 9.8     | 6       |
| 4   | 7.4           | 0.70             | 0.00        | 0.076     | 34.0                 | 0.9978  | 0.58      | 9.4     | 5       |

# Data Preparation

- _Train Test Split_

Train test split aja proses membagi data menjadi data latih dan data uji. Data latih akan digunakan untuk membangun model, sedangkan data uji akan digunakan untuk menguji performa model. Pada proyek ini dataset setelah outliers di drop sebesar **1179** dibagi menjadi **943** untuk data latih dan **236** untuk data uji.

- _Normalization_

Algoritma machine learning akan memiliki performa lebih baik dan bekerja lebih cepat jika dimodelkan dengan data seragam yang memiliki skala relatif sama. Salah satu teknik normalisasi yang digunakan pada proyek ini adalah Standarisasi dengan sklearn.preprocessing.StandardScaler.

|      | alcohol   | sulphates | density   | total sulfur dioxide | chlorides | critic acid | volatile acidity | fixed acidity |
| ---- | --------- | --------- | --------- | -------------------- | --------- | ----------- | ---------------- | ------------- |
| 698  | -0.673854 | -0.875942 | 2.172614  | 1.134441             | 0.575994  | 0.196190    | 0.532994         | 0.862216      |
| 1543 | 0.046702  | -0.527523 | 0.613184  | -0.896516            | -1.016046 | 0.976342    | -0.527436        | 2.033886      |
| 317  | 0.046702  | 0.082209  | 1.275323  | 1.211081             | 0.229898  | -0.695412   | 1.472232         | 1.000060      |
| 940  | 2.105431  | 1.127465  | -0.927681 | -0.666596            | -0.323854 | 1.533593    | -1.193992        | 1.000060      |
| 433  | -0.879727 | -1.224360 | 2.358260  | -0.934836            | 0.852871  | 2.146570    | -0.830416        | 2.860947      |

# Modeling

Algoritma Penelitian ini melakukan pemodelan dengan 3 algoritma, yaitu _K-Nearest Neighbour_, _Random Forest_, dan _Adaboost_

- _K-Nearest Neighbour_ bekerja dengan membandingkan jarak satu sampel ke sampel pelatihan lain dengan memilih sejumlah k tetangga terdekat. Proyek ini menggunakan sklearn.neighbors.KNeighborsRegressor dengan memasukkan X_train dan y_train dalam membangun model. Parameter yang digunakan pada proyek ini adalah :

  - n_neighbors = Jumlah k tetangga tedekat, dimana di proyek ini menggunakan **10**.

- _Random Forest Algoritma_ adalah teknik dalam machine learning dengan metode ensemble. Teknik ini beroperasi dengan membangun banyak decision tree pada waktu pelatihan. Proyek ini menggunakan sklearn.ensemble.RandomForestRegressor dengan memasukkan X_train dan y_train dalam membangun model. Parameter yang digunakan pada proyek ini adalah :

  - n_estimators = Jumlah maksimum estimator di mana boosting dihentikan, Di sini n_estimator= di set menjadi **50**.
  - max_depth = Kedalaman maksimum setiap tree, di proyek ini menggunakan **max_depth = 16**.
  - random_state = Mengontrol seed acak yang diberikan pada setiap base_estimator pada setiap iterasi boosting, di proyek ini menggunakan **random_state = 55**.
  - n_jobs: jumlah job (pekerjaan) yang digunakan secara paralel. Ia merupakan komponen untuk mengontrol thread atau proses yang berjalan secara paralel. **n_jobs=-1** artinya semua proses berjalan secara paralel.

- _Adaboost_ juga disebut _Adaptive Boosting_ adalah teknik dalam _machine learning_ dengan metode ensemble. Algoritme yang paling umum digunakan dengan _AdaBoost_ adalah pohon keputusan (_decision trees_) satu tingkat yang berarti memiliki pohon Keputusan dengan hanya 1 split. Pohon-pohon ini juga disebut _Decision Stumps_. Algoritme ini bertujuan untuk meningkatkan performa atau akurasi prediksi dengan cara menggabungkan beberapa model sederhana dan dianggap lemah (_weak learners_) secara berurutan sehingga membentuk suatu model yang kuat (_strong ensemble learner_). Proyek ini menggunakan sklearn.ensemble.AdaBoostRegressor dengan memasukkan X_train dan y_train dalam membangun model. Parameter yang digunakan pada proyek ini adalah :
  - learning_rate: bobot yang diterapkan pada setiap regressor di masing-masing proses iterasi boosting, pada proyek ini digunakan **learning_rate = 0.05**
  - random_state: digunakan untuk mengontrol random number generator yang digunakan, pada proyek ini digunakan **random_state = 55**

# Evaluation

Metrik evaluasi yang digunakan pada proyek ini adalah akurasi dan _mean squared error (MSE)_. Akurasi menentukan tingkat kemiripan antara hasil prediksi dengan nilai yang sebenarnya (y_test). Mean squared error (MSE) mengukur error dalam model statistik dengan cara menghitung rata-rata error dari kuadrat hasil aktual dikurang hasil prediksi. Berikut formulan MSE :

MSE = $\frac{1}{n} \Sigma_{i=1}^n({y}-\hat{y})^2$

Keterangan:
N = jumlah dataset
yi = nilai sebenarnya
y_pred = nilai prediksi

Berikut ini Hasil evaluasi pada data latih dan data test setiap alogirtme.

| Plugin   | train    | test     |
| -------- | -------- | -------- |
| KNN      | 0.000278 | 0.000757 |
| RF       | 0.000046 | 0.000774 |
| Boosting | 0.000312 | 0.000808 |

Untuk memudahkan, mari kita plot metrik tersebut dengan bar chart.

![akurasi image](https://raw.githubusercontent.com/hadiselamethariyanto/red-wine-quality-machine-learning/main/images/akurasi.png)
Gambar 17

Dari gambar diatas kitab isa melihat bahwa model Random Forest (RF) memiliki nilai error paling kecil dengan tingkat akurasi yang baik, disusul dengan model Boosting. Sedangkan model KNN memiliki nilai error yang tinggi dan tingkat akurasi yang kurang baik.

Model-model tersebut kemudian diuji dengan beberapa data dari dataset untuk mengetahui akurasi model tersebut.

|     | y_true | prediksi_KNN | prediksi_RF | prediksi_Boosting |
| --- | ------ | ------------ | ----------- | ----------------- |
| 211 | 6      | 5.0          | 6.0         | 6.1               |

Pada gambar diatas terlihat bahwa model Random Forest (RF) memberikan nilai yang sama dengan nilai aslinya, sedangkan model Boosting memberikan nilai dengan selisih sedikit, dan untuk model KNN memiliki nilai yang cukup jauh berbeda.
