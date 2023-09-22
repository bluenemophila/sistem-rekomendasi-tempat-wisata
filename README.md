# Laporan Proyek Machine Learning - Shelomita

## Project Overview

Sektor pariwisata merupakan salah satu penopang perekonomian Indonesia, menyumbangkankan 5.0% dari pendapatan domestik bruto (PDB) Indonesia dan memiliki andil besar sebagai sumber devisa utama [1]. Akibat pembatasan di ebrbagai negara akibat pandemi COVID-19 beberapa tahun lalu, kunjungan wisatawan mengalami penurunan yang sangat drastis dan memberikan dampak yang signifikan pada sektor-sektor terkait seperti sektor akomodasi, restoran, maupun transportasi. Namun, di tahun 2023 ini sektor pariwisata telah mengalami pemulihan dan semakin menguat, dan diprediksikan angkanya akan semakin naik hingga tahun 2024 mendatang.

Tercatat pada kuartal pertama tahun 2023, kunjungan wisatawan mancanegara naik drastis sebesar 393.83% dari periode yang sama pada tahun 2022 [2]. Tidak ketinggalan, dari sektor domestik sendiri perjalanan wisatawan lokal telah menyentuh angka 433.57 juta perjalanan selama semester I tahun 2023 [3]. Dalam rangka menjaga kenaikan ini, pemerintah maupun pihak terkait gencar menyusun strategi untuk pengembangan potensi wisata.

Bila dianalisis, kunjungan wisatawan lokal Indonesia terbanyak berada di Provinsi Jawa Timur, disusul Provinsi Jawa Barat, Jawa Tengah, Banten, dan D.I. Yogyakarta. Dengan jumlah wisatawan lokal yang semakin meningkat setiap waktu, diperlukan strategi untuk merekomendasikan destinasi wisata terhadap wisatawan potensial sehingga ketertarikan wisatawan akan semakin meningkat.

## Business Understanding

Dalam merespon peningkatan jumlah wisatawan dan menjaga momentum penguatan pariwisata, terdapat banyak pihak yang dapat ikut serta dalam mewujudkannya. Pemerintah, penyedia paket perjalanan wisata, maupun masyarakat akan mendapatkan keuntungan dengan penerapan rekomendasi destinasi wisata. Beberapa pendekatan dapat dieksplor untuk mendapatkan metode yang terbaik dalam memberikan rekomendasi destinasi wisata kepada wisatawan potensial.

### Problem Statements

Berdasarkan latar belakang tersebut, dapat dirumuskan masalah seperti berikut.
- Bagaimana rekomendasi destinasi wisata dapat membantu meningkatkan kunjungan wisatawan di Indonesia?
- Bagaimana cara untuk membuat model yang dapat memberikan hasil rekomendasi sesuai dengan ketertarikan pengguna?

### Goals

Berdasarkan rumusan masalah tersebut, dapat disusun tujuan dalam melakukan analisis ini seperti berkikut.

- Mengetahui bagaimana rekomendasi destinasi wisata dapat membantu meningkatkan kunjungan wisatawan di Indonesia
- Mendapatkan model yang dapat memberikan rekomendasi yang sesuai dengan ketertarikan pengguna

### Solution statements

Guna menjawab rumusan masalah dan mencapai tujuan tersebut, disusun solusi penyusunan model sistem rekomendasi destinasi wisata dengan langkah-langkah seperti berikut.
1. Pengolahan data
   - Mengumpulkan data destinasi wisata pada daerah yang sering dikunjungi oleh masyarakat
   - Mempersiapkan data dengan preprocessing dan preparation agar dapat dimodelkan dengan sistem rekomendasi yang sesuai
2. Pemodelan
   - Melakukan pembuatan sistem rekomendasi berbasis content based filtering untuk merekomendasikan destinasi wisata berdasarkan kategori yang sesuai
   - Melakukan pembuatan sistem rekomendasi berbasis collaborative filtering untuk merekomendasikan destinasi wisata berdasarkan perilaku pengguna dalam memberikan ulasan pada destinasi wisata

## Data Understanding

Data yang digunakan dalam analisis ini adalah data [Indonesia Tourism Destination](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination?select=tourism_with_id.csv) yang dapat diakses pada _platform_ Kaggle.

Data ini berisi destinasi wisata di 5 kota besar di Indonesia, yaitu Jakarta, Yogyakarta, Semarang, Bandung, dan Surabaya. Dalam data ini terdapat 4 tabel berisi data-data destinasi wisata, yaitu tabel _package_tourism_ yang berisi rekomendasi destinasi wisata, tabel _tourism rating_ yang berisi penilaian destinasi wisata oleh pengguna, tabel _tourism_with_id_ yang berisi data detail mengenai destinasi wisata di 5 kota, dan tabel _user_ yang berisi data pengguna. Dari tabel tersebut masing-masing terdiri dari fitur-fitur seperti di bawah ini.

- Tabel _package tourism_
  | Fitur | Keterangan |
  |-----|-----|
  |Package|ID paket wisata|
  |City|Kota tujuan paket wisata|
  |Place_Tourism1|Destinasi 1 paket wisata|
  |Place_Tourism2|Destinasi 2 paket wisata|
  |Place_Tourism3|Destinasi 3 paket wisata|
  |Place_Tourism4|Destinasi 4 paket wisata|
  |Place_Tourism5|Destinasi 5 paket wisata|
  
- Tabel _tourism rating_
  | Fitur | Keterangan |
  |-----|-----|
  |User_Id|ID pengguna|
  |Place_Id|ID destinasi wisata|
  |Place_Ratings|Ulasan dari destinasi wisata|

- Tabel _tourism with id_
  | Fitur | Keterangan |
  |-----|-----|
  |Place_Id|ID destinasi wisata|
  |Place name|Nama destinasi wisata|
  |Description|Deskripsi destinasi wisata|
  |Category|Kategori destinasi wisata|
  |City|Kota destinasi wisata|
  |Price|Harga tiket masuk|
  |Rating|Ulasan destinasi wisata|
  |Time|Waktu yang dihabiskan saat mengunjungi destinasi wisata|
  |Coordinate|Koordinat lokasi wisata|
  
- Tabel _user_
  | Fitur | Keterangan |
  |-----|-----|
  |User_Id|ID pengguna|
  |Location|Asal pengguna|
  |Age|Usia pengguna|
  
Pada data terdapat 437 destinasi wisata, dengan 10000 ulasan yang ditulis oleh 300 pengguna unik. Terdapat 6 kategori dari destinasi wisata, yaitu kategori budaya, taman hiburan, cagar alam, bahari, pusat perbelanjaan, dan tempat ibadah. Destinasi-destinasi wisata tersebut tersebar dalam 5 kota utama yaitu Jakarta, Yogyakarta, Bandung, Semarang, dan Surabaya.

Berdasarkan letak kotanya, distribusi destinasi wisata dapat dikelompokkan seperti berikut.

![image](https://github.com/bluenemophila/sistem-rekomendasi-tempat-wisata/assets/126690692/fdae7225-e496-4e3e-846a-0f45ecbb65a0)

<p align="center">Gambar 1. Distribusi Destinasi Wisata berdasarkan Letak Kota</p>

Dapat dilihat kota dengan jumlah destinasi wisata terbanyak adalah Kota Yogyakarta disusul oleh Kota Bandung.

Menurut kategorinya, destinasi wisata dapat dikelompokkan seperti berikut.

![image](https://github.com/bluenemophila/sistem-rekomendasi-tempat-wisata/assets/126690692/623b2e11-713d-4345-9bb3-08006a90869c)

<p align="center">Gambar 2. Distribusi Destinasi Wisata berdasarkan Kategori</p>

Dapat dilihat kategori destinasi wisata terbanyak adalah taman hiburan, disusul oleh kategori budaya dan cagar alam.

Untuk melihat berapa banyak antusiasme wisatawan terhadap destinasi wisata, dapat dilihat dari jumlah wisatawan yang meninggalkan ulasan pada lokasi wisata tersebut. Berikut adalah 10 destinasi wisata pada data dengan jumlah ulasan terbanyak.

![image](https://github.com/bluenemophila/sistem-rekomendasi-tempat-wisata/assets/126690692/819e6d1d-3992-440f-8485-a04726c4f666)

<p align="center">Gambar 3. 10 Destinasi Wisata dengan Ulasan Terbanyak</p>

Beberapa hal yang mempengaruhi ketertarikan pengunjung pada destinasi wisata salah satunya adalah harga tiket masuk ke destinasi wisata tersebut. Berikut ini adalah 10 tempat wisata dengan harga tiket masuk tertinggi.

![image](https://github.com/bluenemophila/sistem-rekomendasi-tempat-wisata/assets/126690692/5f25affa-caec-4189-9430-60b131072577)

<p align="center">Gambar 4. 10 Destinasi Wisata dengan Harga Tiket Masuk Tertinggi</p>

Selain mengeksplor dari segi destinasi wisatanya sendiri, dapat dieksplor juga dari segi pengguna yang meninggalkan ulasan di lokasi wisata tersebut. Berikut ini adalah jumlah pengulas berdasarkan kota asalnya.

![image](https://github.com/bluenemophila/sistem-rekomendasi-tempat-wisata/assets/126690692/6f1ff765-1397-4c1a-abac-bf86e5dfccdd)

<p align="center">Gambar 5. Jumlah Pengulas Berdasarkan Kota Asal</p>

Setelah mengamati pola data dan mengeksplorasi strukturnya, dapat dilakukan tahap selanjutnya yaitu persiapan data.

## Data Preparation

### Analisis data hilang dan penghapusan fitur yang tidak diperlukan

Dalam tahap eksplorasi data, terlihat pada variabel _tourism with id_ masih memiliki nilai yang kosong yaitu pada fitur di bawah ini.

|Fitur|Jumlah data hilang|
|-----|-----|
|Time Minutes|232|
|Unnamed: 11|437|

Setelah ditelusuri fitur _Unnamed: 11_ merupakan kolom kosong yang tidak berisi data, sehingga dapat dihapus dari analisis. Fitur _Time Minutes_ merupakan fitur mengenai waktu yang dihabiskan oleh pengunjung di destinasi wisata, sehingga nilainya tidak dapat dibangkitkan. Data yang hilang pada fitur tersebut juga cukup banyak > 50%, sehingga diputuskan untuk menghapusnya dari analisis dikarenakan relevansinya pada sistem rekomendasi yang kurang.

Selain kedua fitur tersebut, terdapat pula fitur _Unnamed: 12_ yang merupakan kolom tanpa identitas. Dikarenakan identitas fitur yang dijelaskan dari kolom tersebut belum jelas, maka kolom tersebut juga dapat dihapus dari analisis.

### Merge dataset

Tahap selanjutnya dari proses persiapan data adalah penggabungan data dari tabel-tabel yang ada. Tabel _tourism rating, tourism with id_ dan tabel _user_ dapat dihubungkan dikarenakan tabel tersebut terdapat relasi antara pengguna yang meninggalkan review pada destinasi wisata yang pernah dikunjungi. Dalam penggabungan tabel, dilakukan penggabungan berdasarkan ID yang sama pada tabel yang berhubungan. Berikut ini adalah relasi dan tabel baru yang dihasilkan dari penggabungan tersebut.

|Relasi|Kunci|Relasi|Tabel baru|
|-----|-----|-----|-----|
|tourism rating & tourism with id|Place id|Ulasan yang ditinggalkan pada destinasi wisata|destination rating|
|destination rating & user rating|User id|Pengguna yang meninggalkan ulasan|user rating|

## Modeling

Dalam menyusun sistem rekomendasi destinasi wisata, dilakukan 2 pendekatan yaitu _content based filtering_ dan _collaborative filtering_. Dengan _content based filtering,_ dapat direkomendasikan destinasi wisata yang serupa berdasarkan lokasi yang pernah diulas oleh pengguna di masa lalu. Sementara itu, untuk _collaborative filtering_ akan digunakan algoritma _neural network_ RecommendationNet untuk menghasilkan serangkaian rekomendasi berdasarkan nilai-nilai ulasan yang ditinggalkan oleh pengguna pada berbagai destinasi wisata di masa lalu.

### Content based filtering

Pada model _content based filtering_ yang digunakan, langkah-langkah pengerjaannya adalah sebagai berikut.

#### Menggunakan TF-IDF Vectorizer

TF-IDF Vectorizer digunakan untuk menemukan representasi fitur penting dari setiap kategori destinasi wisata. Dalam menggunakan TF-IDF Vectorizer, beberapa tahapnya adalah sebagai berikut.
1. Menginisialisasi TF-IDF Vectorizer dari _library_ sklearn
2. Melakukan perhitungan IDF pada data destinasi wisata
3. Melakukan _mapping_ fitur index ke fitur nama desrtinasi kategori
4. Membentuk matriks TF-IDF

Hasil dari TF-IDF Vectorizer tersebut adalah kategori dalam bentuk _array_ seperti berikut ini.

```
array(['bahari', 'budaya', 'cagar_alam', 'pusat_perbelanjaan',
       'taman_hiburan', 'tempat_ibadah'], dtype=object)
```

Setelah dibawa ke dalam bentuk matriks, akan didapatkan nilai-nilai untuk setiap tempat wisata berdasarkan kategorinya. Salah satu contohnya adalah seperti berikut.

|Place_Name|	bahari|	budaya|	cagar_alam|	pusat_perbelanjaan|	taman_hiburan|	tempat_ibadah|
|-----|-----|-----|-----|------|-----|------|		
|Lawang Sewu|	0.0|	1.0|	0.0|	0.0|	0.0|	0.0|
|Curug Cimahi|	0.0|	0.0|	1.0|	0.0|	0.0|	0.0|
|Sea World|	0.0|	0.0|	0.0|	0.0|	1.0|	0.0|

Misalnya dari contoh tersebut, Lawang Sewu termasuk dalam kategori budaya, sementara Curug Cimahi termasuk kategori cagar alam dan selanjutnya.

#### Menggunakan Cosine Similarity

Setelah menerapkan TF-IDF Vectorizer, dapat dihitung derajat kesamaan antara destinasi wisata dengan teknik _cosine similarity._ Setelah menerapkan langkah-langkah _cosine similarity_ akan didapatkan matriks berisi koefisien kesamaan dari destinasi wisata. Contonya adalah sepeti berikut.

|Place_Name|	Monumen Nasional|	Kota Tua|	Dunia Fantasi|	Taman Mini Indonesia Indah (TMII)|	Atlantis Water Adventure|
|-----|-----|-----|-----|------|-----|
|Kota Mini|	0.0|	0.0|	1.0|	1.0|	1.0|

Dari contoh tersebut berarti Kota Mini memiliki kesamaan dengan Dunia Fantasi, TMII, Atlantis Water Adventure, dan Ancol.

#### Mendapatkan rekomendasi

Setelah memiliki data kesamaan antara destinasi wisata, dapat digunakan untuk membentuk rekomendasi pada pengguna. Dibuat fungsi seperti di bawah ini.

```
def destination_recommendations(place_name, similarity_data=cosine_sim, items=tourism_with_id[['Place_Name', 'City', 'Category']], k=10):
    index = similarity_data.loc[:,place_name].to_numpy().argpartition(range(-1, -k, -1))
    closest = similarity_data.columns[index[-1:-(k+2):-1]]
    closest = closest.drop(place_name, errors='ignore')
    return pd.DataFrame(closest).merge(items).head(k)
```

Parameter dari fungsi tersebut adalah
- place_name : Nama destinasi wisata
- similarity_data : _Dataframe_ kesamaan yang telah didefinisikan dengan _cosine similarity_ sebelumnya
- items : Nama dan fitur yang digunakan untuk mendefinisikan kemiripan
- k : Banyak rekomendasi yang ingin diberikan, dalam kasus ini digunakan sebanyak 10 rekomendasi

Setelah dijalankan proses rekomendasinya, dapat dimasukkan nama destinasi wisata ke dalam fungsi tersebut untuk mendapatkan 10 rekomendasi tempat wisata yang mirip.

Bererapa contohnya adalah sebagai berikut.

Input : Kategori Budaya

```destination_recommendations('Monumen Nasional')```

Rekomendasi :
|Place_Name	|City	|Category|
|-----|-----|-----|
|Bandros City Tour|	Bandung|	Budaya|
|Saung Angklung Mang Udjo|	Bandung	|Budaya|
|Museum Satria Mandala|	Jakarta|	Budaya|
|Keraton Yogyakarta|	Yogyakarta|	Budaya|
|Museum Benteng Vredeburg Yogyakarta|	Yogyakarta|	Budaya|
|Candi Sewu|	Yogyakarta|	Budaya|
|Kyotoku Floating Market|	Bandung|	Budaya|
|Museum Nike Ardilla|	Bandung|	Budaya|
|Taman Budaya Yogyakarta|	Yogyakarta|	Budaya|
|Kampung Wisata Sosro Menduran|	Yogyakarta|	Budaya|

Input : Kategori Bahari

```destination_recommendations('Pantai Cipta')```

|Place_Name	|City	|Category|
|-----|-----|-----|
|Pantai Pok Tunggal|	Yogyakarta|	Bahari|
|Pantai Nguluran|	Yogyakarta|	Bahari|
|Pantai Samas|	Yogyakarta|	Bahari|
|Pantai Drini|	Yogyakarta|	Bahari|
|Pantai Sadranan|	Yogyakarta|	Bahari|
|Pantai Jungwok|	Yogyakarta|	Bahari|
|Pantai Wediombo|	Yogyakarta|	Bahari|
|Pantai Goa Cemara|	Yogyakarta|	Bahari|
|Pantai Timang|	Yogyakarta|	Bahari|
|Pantai Ngrenehan|	Yogyakarta|	Bahari|

Dari hasil _content based filtering_ tersebut telah dihasilkan rekomendasi yang cukup baik dengan kategori yang sama seperti kategori yang dijadikan input. Untuk evaluasi dari model ini akan dilanjutkan di bagian selanjutnya.

### Collaborative filtering

Pada model _collaborative filtering_ yang digunakan, tahapannya adalah sebagai berikut.

#### Persiapan data

Pertama-tama sebelum melakukan pemodelan, fitur 'user id' dan 'place id' harus disandikan (encoding) terlebih dahulu menjadi indeks _integer._ Beberapa hasilnya adalah seperti berikut.

```
list User ID :  [36, 38, 64, ...]
encoded user ID :  {36: 0, 38: 1, 64: 2, ...}
encoded angka ke user ID:  {0: 36, 1: 38, 2: 64, ...}
```

Selanjutnya, dipetakan 'user id' dan 'place id' ke tabel yang berkaitan, lalu mengubah data-data numerik menjadi tipe data _float._

Setelah menyelesaikan langkah tersebut, dilakukan pembagian data menjadi 80% data latih dan 20% data uji. Hal ini dilakukan supaya model dapat diuji terhadap data yang belum pernah dilihat sebelumnya. Melakukan pembagian tersebut juga berfungsi untuk menghindari _overfitting,_ yaitu akurasi yang tinggi ketika digunakan untuk memodelkan data latih, namun performanya buruk jika memodelkan data yang belum pernah dilihat sebelumnya.

#### Proses training

Dalam memodelkan dengan _collaborative filtering_ digunakan algoritma RecommenderNet dari _library_ model keras Tensorflow. Di dalam fungsi pemodelan ini dilakukan operasi perkalian _dot product_ terhadap _embedding_ pengguna dan destinasi wisata. Selain itu ditambahkan pula bias untuk setiap pengguna dan destinasi wisata. Skor kecocokan selanjutnya ditetapkan dalam skala [0,1] dengan fungsi aktivasi sigmoid.

Selanjutnya dilakukan proses _compile_ terhadap model, 

```
model = RecommenderNet(num_users, num_destination, 50)
 
model.compile(
    loss = tf.keras.losses.BinaryCrossentropy(),
    optimizer = keras.optimizers.Adam(learning_rate=0.001),
    metrics=[tf.keras.metrics.RootMeanSquaredError()]
)
```

Digunakan Binary Crossentropy untuk menghitung _loss function_, Adam (Adaptive Moment Estimation) sebagai _optimizer) dan RMSE sebagai metriks evaluasi.

Selanjutnya dapat dimulai proses training.

```
history = model.fit(
    x = x_train,
    y = y_train,
    epochs = 100,
    validation_data = (x_val, y_val)
)
```

Digunakan ukuran _epoch_ sebanyak 100 _epoch_ dalam proses tersebut. Sebagian _outpunya_ adalah sebagai berikut.

```
Epoch 98/100
250/250 [==============================] - 0s 1ms/step - loss: 0.6674 - root_mean_squared_error: 0.3256 - val_loss: 0.7154 - val_root_mean_squared_error: 0.3632
Epoch 99/100
250/250 [==============================] - 0s 1ms/step - loss: 0.6675 - root_mean_squared_error: 0.3257 - val_loss: 0.7156 - val_root_mean_squared_error: 0.3633
Epoch 100/100
250/250 [==============================] - 0s 1ms/step - loss: 0.6677 - root_mean_squared_error: 0.3258 - val_loss: 0.7156 - val_root_mean_squared_error: 0.3633
```

Hasil plot metriks dapat dievaluasi untuk melihat apakah proses training sudah berjalan dengan baik.

#### Mendapatkan rekomendasi destinasi wisata

Untuk mendapatkan rekomendasi wisata untuk pengguna, terlebih dahulu dilakukan pembagian data destinasi wisata yang telah dikunjungi oleh pengguna dan destinasi yang belum dikunjungi. Destinasi yang telah dikunjungi tersebut kemudian diurutkan berdasarkan ulasan tertinggi yang ditinggalkan oleh pengguna. Berikut adalah salah satu contoh rekomendasi yang diberikan pada pengguna.

```
Daftar rekomendasi destinasi wisata untuk: User 144
============================================= 

------------------------------------------------------------
Tempat dengan rating wisata paling tinggi dari user
------------------------------------------------------------
Sea World : Taman_Hiburan
Bukit Wisata Pulepayung : Cagar_Alam
Bandros City Tour : Budaya
Pantai Marina : Bahari
Wisata Lereng Kelir : Cagar_Alam

------------------------------------------------------------
7 Rekomendasi tempat wisata teratas
------------------------------------------------------------
1 . Kampung Cina 
     Jakarta , Budaya , Harga Tiket Masuk  15000 , Rating Wisata  4.5 

2 . Air Terjun Kedung Pedut 
     Yogyakarta , Cagar_Alam , Harga Tiket Masuk  20000 , Rating Wisata  4.5 

3 . Puncak Gunung Api Purba - Nglanggeran 
     Yogyakarta , Cagar_Alam , Harga Tiket Masuk  10000 , Rating Wisata  4.7 

4 . Pantai Baron 
     Yogyakarta , Bahari , Harga Tiket Masuk  10000 , Rating Wisata  4.4 

5 . Dago Dreampark 
     Bandung , Taman_Hiburan , Harga Tiket Masuk  40000 , Rating Wisata  4.2 

6 . Teras Cikapundung BBWS 
     Bandung , Taman_Hiburan , Harga Tiket Masuk  0 , Rating Wisata  4.3 

7 . Keraton Surabaya 
     Surabaya , Budaya , Harga Tiket Masuk  0 , Rating Wisata  4.4 

=============================================
```

## Evaluation

### Content based filtering

Dalam mengevaluasi model yang telah dihasilkan dari algoritma _content based filtering,_ dapat digunakan persamaan berikut.

$`presisi sistem rekomendasi : P = \frac{jumlah rekomendasi yang relevan}{jumlah item rekomendasi}`$

Misalkan dari contoh yang dihasilkan,

Rekomendasi untuk `destination_recommendations('Hutan Bambu Keputih')`, kategori cagar alam.

|Place_Name	|City	|Category|
|-----|-----|-----|
|Tebing Karaton|	Bandung|	Cagar_Alam|
|Situ Cileunca|	Bandung|	Cagar_Alam|
|Sunrise Point Cukul|	Bandung|	Cagar_Alam|
|Lereng Anteng Panoramic Coffee Place|	Bandung|	Cagar_Alam|
|The Lodge Maribaya|	Bandung	|Cagar_Alam|
|Observatorium Bosscha|	Bandung|	Cagar_Alam|
|Taman Bunga Cihideung|	Bandung|	Cagar_Alam|
|Perkebunan Teh Malabar|	Bandung|	Cagar_Alam|
|Sungai Palayangan|	Bandung|	Cagar_Alam|
|Babakan Siliwangi City Forest Path Bandung|	Bandung|	Cagar_Alam|

Dari hasil tersebut diketahui

$`presisi sistem rekomendasi : P = \frac{jumlah rekomendasi yang relevan}{jumlah item rekomendasi} = \frac{7}{7}`$

Presisi sistem rekomendasi yang dihasilkan adalah 100%, dimana telah direkomendasikan 10 destinasi wisata dengan kategori yang sesuai dengan kategori yang diinginkan pengguna. Hal ini dapat dilihat juga dari contoh yang telah diberikan pada bagian sebelumnya.

### Collaborative filtering

Untuk mengevaluasi model yang dihasilkan dari algoritma _collaborative filtering,_ dapat dilakukan _plotting_ antara jumlah epoch dan RMSEnya.

RMSE merupakan metode pengukuran kesalahan dengan menghitung selisih antara prediksi dari model dengan nilai sebenarnya. Semakin kecil RMSE, maka model tersebut akan semakin akurat. Menggunakan RMSE memiliki kelebihan yaitu memberikan penalti yang besar pada kesalahan prediksi yang besar, sehingga penerapannya lebih efektif pada beberapa kasus tertentu saja.

Formula RMSE adalah sebagai berikut.

$`RMSE = \sqrt{\frac{1}{n}\Sigma_{i=1}^{n}{\Big(\frac{d_i -f_i}{\sigma_i}\Big)^2}}`$

Dihasilkan grafik evaluasi training seperti berikut.


![image](https://github.com/bluenemophila/sistem-rekomendasi-tempat-wisata/assets/126690692/bba2f97d-da3c-4e75-85e6-a946e61cb529)

<p align="center">Gambar 6. Plot Evaluasi Hasil Training</p>

Dapat dilihat, proses training model cukup _smooth_ dan model konvergen di sekitar _epoch_ 100. Dari proses tersebut, terlihat error akhir sebesar 0.32 untuk data latih dan 0.36 untuk data uji.

# Referensi

[1] C. Puwowidhu, “Kian Melesat di 2023, Pariwisata Indonesia Bersiap Menuju Level Prapandemi” Media Keuangan Kemenkeu, https://mediakeuangan.kemenkeu.go.id/article/show/kian-melesat-di-2023-pariwisata-indonesia-bersiap-menuju-level-prapandemi (accessed Sep. 20, 2023). \
[2] “Peningkatan kunjungan wisatawan mancanegara pada April 202,” Badan Pusat Statistik, https://www.bps.go.id/pressrelease/2023/06/05/1978/peningkatan-kunjungan-wisatawan-mancanegara-pada-april-2023-yang-tumbuh-276-31-persen-dibandingkan-april-2023-dan-jumlah-penumpang-angkutan-laut-dalam-negeri-pada-april-2023-naik-24-75-persen.html (accessed Sep. 20, 2023). \
[3] “Kunjungan Wisatawan Mancanegara Indonesia Juni 2023,” Badan Pusat Statistik, https://www.bps.go.id/pressrelease/2023/08/01/1980/kunjungan-wisatawan-mancanegara-pada-juni-2023-tumbuh-119-64-persen-bila-dibandingkan-bulan-yang-sama-pada-tahun-lalu-dan-jumlah-penumpang-angkutan-udara-internasional-pada-juni-2023-naik-10-66-persen.html (accessed Sep. 20, 2023). 
