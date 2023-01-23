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

![cover image](https://raw.githubusercontent.com/hadiselamethariyanto/movie-recommendation/main/images/dataset-cover.jpg)
Gambar 1: cover

Dataset yang digunakan dalam proyek ini bisa didapatkan di [Kaggle: Movie Recommender System Dataset](https://www.kaggle.com/datasets/gargmanas/movierecommenderdataset).

**Berikut informasi pada dataset:**

- Dataset memiliki format CSV
- Memiliki 2 berkas csv, yakni movies.csv dan ratings.csv
- movies.csv memiliki 9.742 data sedangkan ratings.csv memiliki 610 data

**Variable – variable pada dataset**
**movies.csv**

- movieId: id setiap film
- title: judul film
- genres: jenis kategori film

**ratins.csv**

- userId: id setiap user yang memberikan rating
- movieId: id setiap film
- rating: nilai yang diberikan user untuk setiap film
- timestamp: waktu user memberikan rating

### Exploratory Data Analysis

![number movie genre](https://raw.githubusercontent.com/hadiselamethariyanto/movie-recommendation/main/images/newplot.png)
Gambar 2

pada gambar 2 dapat dilihat bahwa Drama, Commedy dan action menjadi genre dengan film terbanyak, sedangkan Documentary, Film-noir dan Western menjadi genre dengan film tersedikit.

![number of movies each year](<https://raw.githubusercontent.com/hadiselamethariyanto/movie-recommendation/main/images/newplot(1).png>)
Gambar 3

pada Gambar 3 dapat dilihat grafik jumlah film yang direlease setiap tahun, dan tahun 1995 menjadi tahun dengan film terbanyak.

![top 15 movie highest](<https://raw.githubusercontent.com/hadiselamethariyanto/movie-recommendation/main/images/newplot(3).png>)
Gambar 4
pada Gambar 4 dapat dilihat 15 film teratas dengan rating tertinggi.

![top 15 movie smallest](<https://raw.githubusercontent.com/hadiselamethariyanto/movie-recommendation/main/images/newplot(4).png>)
Gambar 5
pada Gambar 5 dapat dilihat 15 film terbawah dengan rating terendah.

![top 15 genres highest](<https://raw.githubusercontent.com/hadiselamethariyanto/movie-recommendation/main/images/newplot(5).png>)
Gambar 6
pada Gambar 6 dapat dilihat 15 genre teratas dengan rating tertinggi. disini dapat dilihat, meskipun jumlah film dengan genre docummentary sedikit, akan tetapi memiliki rating yang bagus.

![top 15 genres smallest](<https://raw.githubusercontent.com/hadiselamethariyanto/movie-recommendation/main/images/newplot(6).png>)
Gambar 7
pada Gambar 7 dapat dilihat 15 genre terbawah dengan rating terendah. dapat dilihat bahwa film dengan genre action mendominasi rating terendah.

# Data Preparation

**content based filtering**
pada algoritme ini, dilakukan beberapa persiapan pada data sebelum diproses.

- Melakukan pengencekan missing value
- Menggabungkan data ratings dengan movies berdasarkan nilai movieId
- memisahkan tahun yang ada pada kolom title ke kolom tersendiri yaitu kolom _year_
- menghapus tahun pada judul film
- menghapus data rating yang tidak bertipe integer
- menghapus data dengan jumlah rating dibawah 10
- melakukan sorting data berdasarkan movieId seacara _ascending_
- menghapus duplikat film
- mengkonversi data series movieId, title, dan genre menjadi list
- membuat dictionary untuk data movie_id, movie_name, dan movie_genre

**collaborative filtering**
pada algoritme ini juga dilakukan persiapan data sebelum dilakukan modelling.

- Menyandikan (encode) fitur 'userID ' dan ' movieID' ke dalam indeks integer dengan cara mengubah userID dan movie menjadi list tanpa nilai yang sama, melakukan encoding userID dan movieID serta melakukan proses encoding angka ke userID dan movieID
- Memetakan ‘userID’ dan ‘movieID’ ke dataframe yang berkaitan.
- Mengecek beberapa hal dalam data seperti jumlah user, jumlah movie, kemudian mengubah nilai rating menjadi float, mendapatkan nilai rating minimum dan maximum

# Modeling

---

##### **Content Based filtering**

- Melakukan Teknik TF-IDF Vectorizer untuk menemukan representasi fitur penting dari setiap kategori movie dan genre

| movie_name                            | crime               | action              | fantasy             | horror | children            | imax | comedy               | film | musical | romance             | drama               | mystery | documentary | noir | sci                 | adventure          | war                 | animation | fi                  | thriller            |
| ------------------------------------- | ------------------- | ------------------- | ------------------- | ------ | ------------------- | ---- | -------------------- | ---- | ------- | ------------------- | ------------------- | ------- | ----------- | ---- | ------------------- | ------------------ | ------------------- | --------- | ------------------- | ------------------- |
| Saving Private Ryan                   | 0\.0                | 0\.4469716450168563 | 0\.0                | 0\.0   | 0\.0                | 0\.0 | 0\.0                 | 0\.0 | 0\.0    | 0\.0                | 0\.3709645261012112 | 0\.0    | 0\.0        | 0\.0 | 0\.0                | 0\.0               | 0\.8140034821334791 | 0\.0      | 0\.0                | 0\.0                |
| Driving Miss Daisy                    | 0\.0                | 0\.0                | 0\.0                | 0\.0   | 0\.0                | 0\.0 | 0\.0                 | 0\.0 | 0\.0    | 0\.0                | 1\.0                | 0\.0    | 0\.0        | 0\.0 | 0\.0                | 0\.0               | 0\.0                | 0\.0      | 0\.0                | 0\.0                |
| Jerk, The                             | 0\.0                | 0\.0                | 0\.0                | 0\.0   | 0\.0                | 0\.0 | 1\.0                 | 0\.0 | 0\.0    | 0\.0                | 0\.0                | 0\.0    | 0\.0        | 0\.0 | 0\.0                | 0\.0               | 0\.0                | 0\.0      | 0\.0                | 0\.0                |
| Addams Family Values                  | 0\.0                | 0\.0                | 0\.6322502323811345 | 0\.0   | 0\.6736877096166014 | 0\.0 | 0\.38262842754497356 | 0\.0 | 0\.0    | 0\.0                | 0\.0                | 0\.0    | 0\.0        | 0\.0 | 0\.0                | 0\.0               | 0\.0                | 0\.0      | 0\.0                | 0\.0                |
| Salt                                  | 0\.0                | 0\.6924400514020411 | 0\.0                | 0\.0   | 0\.0                | 0\.0 | 0\.0                 | 0\.0 | 0\.0    | 0\.0                | 0\.0                | 0\.0    | 0\.0        | 0\.0 | 0\.0                | 0\.0               | 0\.0                | 0\.0      | 0\.0                | 0\.7214754155301056 |
| Eternal Sunshine of the Spotless Mind | 0\.0                | 0\.0                | 0\.0                | 0\.0   | 0\.0                | 0\.0 | 0\.0                 | 0\.0 | 0\.0    | 0\.5153078693141716 | 0\.3591328550074244 | 0\.0    | 0\.0        | 0\.0 | 0\.5502187711615739 | 0\.0               | 0\.0                | 0\.0      | 0\.5502187711615739 | 0\.0                |
| Mississippi Burning                   | 0\.6962055625241071 | 0\.0                | 0\.0                | 0\.0   | 0\.0                | 0\.0 | 0\.0                 | 0\.0 | 0\.0    | 0\.0                | 0\.4472504759676197 | 0\.0    | 0\.0        | 0\.0 | 0\.0                | 0\.0               | 0\.0                | 0\.0      | 0\.0                | 0\.5614844846095297 |
| Logan's Run                           | 0\.0                | 0\.4266426698478334 | 0\.0                | 0\.0   | 0\.0                | 0\.0 | 0\.0                 | 0\.0 | 0\.0    | 0\.0                | 0\.0                | 0\.0    | 0\.0        | 0\.0 | 0\.5424965260187203 | 0\.478926999427212 | 0\.0                | 0\.0      | 0\.5424965260187203 | 0\.0                |
| 28 Days                               | 0\.0                | 0\.0                | 0\.0                | 0\.0   | 0\.0                | 0\.0 | 0\.0                 | 0\.0 | 0\.0    | 0\.0                | 1\.0                | 0\.0    | 0\.0        | 0\.0 | 0\.0                | 0\.0               | 0\.0                | 0\.0      | 0\.0                | 0\.0                |
| Nosferatu                             | 0\.0                | 0\.0                | 0\.0                | 1\.0   | 0\.0                | 0\.0 | 0\.0                 | 0\.0 | 0\.0    | 0\.0                | 0\.0                | 0\.0    | 0\.0        | 0\.0 | 0\.0                | 0\.0               | 0\.0                | 0\.0      | 0\.0                | 0\.0                |

- Menghitung derajat kesamaan (similarity degree) antar movie dengan teknik cosine similarity

![cosine_similiarity](https://raw.githubusercontent.com/hadiselamethariyanto/movie-recommendation/main/images/cosine_similiarity.png)
Gambar 8: derajat kesamaan antar movie

| movie_name                            | Enemy at the Gates   | Beautiful Mind, A    | The Butterfly Effect | For Your Eyes Only   | Time Bandits         |
| ------------------------------------- | -------------------- | -------------------- | -------------------- | -------------------- | -------------------- |
| Airheads                              | 0\.0                 | 0\.0                 | 0\.0                 | 0\.0                 | 0\.3181208170551465  |
| Air Force One                         | 0\.0                 | 0\.0                 | 0\.33591086252839847 | 0\.7895359864684683  | 0\.0                 |
| I Now Pronounce You Chuck and Larry   | 0\.0                 | 0\.6665058003015498  | 0\.0                 | 0\.0                 | 0\.18549559968350032 |
| Harry Potter and the Sorcerer's Stone | 0\.0                 | 0\.0                 | 0\.0                 | 0\.29322876679723064 | 0\.5156267573220966  |
| Mulholland Drive                      | 0\.08087521309465465 | 0\.11150854739243288 | 0\.18631979881716737 | 0\.1394656262696644  | 0\.0                 |
| American Graffiti                     | 0\.2888873383957831  | 0\.39831001652976267 | 0\.2583541239849375  | 0\.0                 | 0\.22823076172920503 |
| Matrix Revolutions, The               | 0\.0                 | 0\.0                 | 0\.6068742129567533  | 0\.5751340791274846  | 0\.525887247388291   |
| Star Trek Into Darkness               | 0\.0                 | 0\.0                 | 0\.480879738300071   | 0\.4112089563911724  | 0\.5566053937906993  |
| Back to the Future                    | 0\.0                 | 0\.0                 | 0\.632181461378334   | 0\.3014029058331367  | 0\.8506955593398626  |
| Cutting Edge, The                     | 0\.20431852895372787 | 0\.861703167139819   | 0\.18272360033104856 | 0\.0                 | 0\.1614185438429053  |

Table 2: hasil similarity matrix pada setiap movie

- Mendapatkan rekomendasi

| index | id  | movie_name   | genre                                   |
| ----- | --- | ------------ | --------------------------------------- |
| 178   | 356 | Forrest Gump | Comedy&#124;Drama&#124;Romance&#124;War |

Table 3: pengecekan data forrest gump pada dataset

| index | movie_name            | genre                                   |
| ----- | --------------------- | --------------------------------------- |
| 0     | Life Is Beautiful     | Comedy&#124;Drama&#124;Romance&#124;War |
| 1     | Atonement             | Drama&#124;Romance&#124;War             |
| 2     | From Here to Eternity | Drama&#124;Romance&#124;War             |
| 3     | English Patient, The  | Drama&#124;Romance&#124;War             |
| 4     | Doctor Zhivago        | Drama&#124;Romance&#124;War             |
| 5     | Gone with the Wind    | Drama&#124;Romance&#124;War             |
| 6     | Cold Mountain         | Drama&#124;Romance&#124;War             |
| 7     | Mister Roberts        | Comedy&#124;Drama&#124;War              |
| 8     | Good Morning, Vietnam | Comedy&#124;Drama&#124;War              |
| 9     | M\*A\*S\*H            | Comedy&#124;Drama&#124;War              |

Table 4: Hasil rekomendasii film forrest gump

---

##### **Collaborative filtering**

Pada bagian ini dilakukan modelling dengan Collaborative filtering memakai pendekatan _deep learning_, dengan urutan modelling sebagai berikut :

- Melakukan pengacakan data agar distribusinya menjadi random
- Membuat variabel x untuk mencocokkan data user dan movie menjadi satu value dan y untuk membuat rating dari hasil
- melakukan pembagian data menjadi data training dan validasi dengan proporsi 80:20
- Setelah itu dilakukan pembuatan model untuk menghitung skor kecocokan antara user dan movie dengan teknik embedding.
- Melakukan proses _compile_ pada model
- Melakukan proses training model dengan _epoch_ 100
- Membuat kelas untuk mengambil sampel user secara acak dan definisikan variabel movie_not_visited sebagai sebagai daftar movie untuk direkomendasikan pada pengguna.
- memperoleh rekomendasi movie, gunakan fungsi model.predict() dari library Keras
- Visualisasi plot metrik evaluasi dengan matplotlib

| Showing recommendations for users: 357                                                     |
| ------------------------------------------------------------------------------------------ | --------- | -------- | ------- | ------- | -------- |
| ===========================                                                                |
| Movie with high ratings from user                                                          |
| --------------------------------                                                           |
| Toy Story (1995) : Adventure                                                               | Animation | Children | Comedy  | Fantasy |
| Tombstone (1993) : Action                                                                  | Drama     | Western  |
| To Kill a Mockingbird (1962) : Drama                                                       |
| Goodfellas (1990) : Crime                                                                  | Drama     |
| Capturing the Friedmans (2003) : Documentary                                               |
| --------------------------------                                                           |
| Top 10 movie recommendation                                                                |
| --------------------------------                                                           |
| Heidi Fleiss: Hollywood Madam (1995) : Documentary                                         |
| Jonah Who Will Be 25 in the Year 2000 (Jonas qui aura 25 ans en l'an 2000) (1976) : Comedy |
| Stunt Man, The (1980) : Action                                                             | Adventure | Comedy   | Drama   | Romance | Thriller |
| Belle époque (1992) : Comedy                                                               | Romance   |
| Trial, The (Procès, Le) (1962) : Drama                                                     |
| Adam's Rib (1949) : Comedy                                                                 | Romance   |
| Enter the Void (2009) : Drama                                                              |
| Terri (2011) : Comedy                                                                      |
| Maniac Cop 2 (1990) : Action                                                               | Horror    | Thriller |
| Stuart Little 3: Call of the Wild (2005) : Animation                                       | Children  | Comedy   | Fantasy |

Table 5: hasil rekomendasi menggunakan algoritme _content based filtering_

# Evaluation

#### **Content based filtering**

Metric yang digunakan pada sistem rekomendasi judul film berdasarkan teknik **Content based filtering** adalah accuracy precision. Precision adalah metrik yang membandingkan rasio prediksi benar atau positif dengan keseluruhan hasil yang diprediksi positif dengan rumus

```python
Precission = (TP) / (TP+FP).

keterangan:
TP = True Positif (prediksi positif dan hal tersebut benar)
FP = False Negatif (prediksi positif dan hal tersebut salah)
```

#### **Collaborative filtering**

Dalam proyek ini, digunakan Root Mean Squared Error (RMSE) sebagai metrik evaluasi untuk mengukur kinerja model menggunakan pendekatan pembelajaran mendalam untuk sistem rekomendasi. Root mean squared error (RMSE) adalah metrik yang mengukur perbedaan antara nilai prediksi model sebagai perkiraan nilai yang diamati. Root mean squared error adalah hasil dari akar kuadrat dari mean squared error. Keakuratan metode estimasi kesalahan pengukuran ditunjukkan dengan adanya nilai RMSE yang kecil. Metode estimasi dengan root mean square error (RMSE) yang kecil dikatakan lebih akurat daripada metode estimasi dengan root mean square error yang besar (RMSE). Metode yang digunakan untuk menghitung root-mean-square error (RMSE) adalah dengan mengurangkan nilai aktual dari nilai prediksi, kemudian kuadratkan dan bagi jumlah dengan jumlah data. Hasil perhitungan tersebut dihitung ulang untuk mencari nilai akar kuadrat. Di bawah ini adalah rumus untuk menghitung RSME.

RMSE = \sqrt{\frac{1}{n}\Sigma\_{i=1}^{n}{\Big(\frac{d_i -f_i}{\sigma_i}\Big)^2}}

Berikut merupakan visualisai metrik pada proses training terhadap model Deep Learning sebelumnya:

![This is an image](https://raw.githubusercontent.com/hadiselamethariyanto/movie-recommendation/main/images/model_metrics.png)

Gambar 9 : Visualisasi plot _metric_

Pada gambar 9 menunjukkan bahwa model mempunyai nilai **root_mean_squared_error** sebesar 0.1944 dengan nilai loss yang diperoleh sebanyak 0.6045 , hasil tersebut sudah cukup bagus karena dengan nilai root_mean_squared_error sebesar 0.1944 berarti perbedaan nilai dari prediksi sebuah model sebagai estimasi atas nilai yang diobservasi sebesar 0.1944
