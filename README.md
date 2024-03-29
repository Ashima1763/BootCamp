# Laporan Proyek Akhir Machine Learning - Maulana Muhammad

## Parawisata - Rekomendasi Destinasi Wisata Turis di Indonesia

![indonesia-travel-attraction-landmarks-tourism-traditional-culture-91162722](https://user-images.githubusercontent.com/58927608/229541740-616aef88-1faa-4d1c-8859-d34a30e9f412.jpg)
[Sumber Gambar](https://www.dreamstime.com/stock-illustration-indonesia-travel-attraction-landmarks-tourism-traditional-culture-image91162722)

Pariwisata merupakan salah satu sektor yang menghasilkan devisa negara terbanyak dan sektor ini berperan penting dalam meningkatkan perekonomian suatu negara. Sektor pariwisata merupakan salah satu sektor strategis yang harus dimanfaatkan untuk pembangunan kepariwisataan sebagai mana bagian dari pembangunan Nasional. Pengaruh pariwisata terhadap ekonomi dengan menganalisis jumlah turis dan devisa pariwisata di Indonesia pada tahun 2014 menunjukan pertumbuhan pariwisata (devisa pariwisata dan jumlah turis) dan nilai tukar rupiah memiliki peningkatan kurs. Perkembangan pariwisata di Indonesia diikuti dengan jumlah turis kunjungan turis yang meningkat. Pada tahun 2013 terjadi peningkatan sektor pariwisata yang sebelumnya dari 10%  menjadi 17% dari total ekspor barang dan jasa dengan penghasilan 10 Miliyar USD. Data pada tahun 2022 Badan Pusat Statistik (BPS) mencatat turis yang datang ke Indonesia naik menjadi 364%, hal ini jelas merupakan kenaikan yang sangat tinggi, dan dapat dipastikan tiap tahunnya akan ada peningkatan kenaikan kunjungan turis ke Indonesia.

## Business Understanding

Pariwisata atau turisme adalah suatu perjalanan yang dilakukan untuk rekreasi atau liburan dan juga persiapan yang dilakukan untuk aktivitas ini. Sedangkan seorang wisatawan atau biasa disebut tirus merupakan seorang yang melakukan perjalanan setidaknya paling tidak sejauh 80 km dari tempat tinggalnya. Parawisata di Indonesia merupakan sektor penting karena sektor ini merupakan salah satu penyumpang devisa negara yang paling besar. Untuk para wisatawan atau turis melakukan wisata di Indonesia merupakan hal yang menyenangkan karena banyaknya wisata di Indonesia seakan tidak ada habisnya. Karena keanekaragaman wisata di Indonesia sangat banyak, ini juga dapat menimbulkan masalah, karena wisatawan atau turis yang ingin melakukan perjalanan wisata menjadi bingung untuk memulai dari mana. Oleh karena itu dibuatlah sistem rekomendasi untuk merekomendasikan wisatawan atau turis berdasarkan informasi masa lalu yaitu berupa tempat wisata yang pernah dikunjungi dan rekomendasi berdasarkan rating dari tempat wisata.

### Problem Statement

Menjelaskan pernyataan masalah latar belakang:
- Berdasarkan data wisatawan atau turis, bagaimana membuat sistem rekomendasi yang dipersonalisasi dengan teknik *content-based filtering?*
- Dengan data rating dari wisatawan atau turis, bagaimana cara untuk merekomendasikan destinasi wisata lain yang mungkin disukai oleh wisatawan atau turis yang tidak pernah mengunjungi tempat tersebut?

### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Menghasilkan rekomendasi destinasi parawisata yang dipersonalisasi untuk wisatawan atau turis dengan *content-based filtering*.
- Menghasilkan rekomendasi destinasi wisata yang sesuai dengan preferensi wisatawan atau turis yang belum pernah dikunjungi sebelumnya dengan *collaborative filtering*.

    ### Solution statements
    - Menggunakan *cosine similarity* untuk melakukan rekomendasi *content-based filtering* dengan mencari kemaripan antar data.
    - Membuat class RecommenderNet dengan keras Model Class untuk melakukan rekomendasi menggunakan *collaborative filtering* berdasarkan rating wisatawan atau turis. 

## Data Understanding
Dataset : [Indonesia Tourism Destination](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination)

**Overview**

- Nama dataset : Indonesia Tourism Destination
- Jumlah file terdiri dari :
  - package_tourism.csv
  - tourism_rating.csv
  - tourism_with_id.csv
  - user.csv
- Jumlah kolom terdiri dari :
  - package_tourism.csv : 7
  - tourism_rating.csv : 3
  - tourism_with_id.csv : 12
  - user.csv : 3
- Jumlah data terdiri dari : 
  - package_tourism.csv : 100
  - tourism_rating.csv : 10000
  - tourism_with_id.csv : 437
  - user.csv : 300
- Usability : 8.24
- License : Data files © Original Authors (A_PRABOWO)
- Date Updated : 21 July 2021

### Variabel-variabel pada Indonesia Tourism Destination dataset adalah sebagai berikut:
*   Variabel pada package_tourism.csv
    *   Package : Paket destinasi wisata
    *   City : Kota pada paket destinasi wisata
    *   Place_Tourism1 : Tempat destinasi wisata pertama
    *   Place_Tourism2 : Tempat destinasi wisata kedua
    *   Place_Tourism3 : Tempat destinasi wisata ketiga
    *   Place_Tourism4 : Tempat destinasi wisata keempat
    *   Place_Tourism5 : Tempat destinasi wisata kelima
*   Variabel pada tourism_rating.csv
    *   User_Id : Id wisatawan atau turis
    *   Place_Id : Id tempat wisata
    *   Place_Ratings : Rating tempat wisata
*   Variabel pada tourism_with_id.csv
    *   Place_Id : Id tempat wisata
    *   Place_Name : Nama tempat wisata
    *   Description : Deskripsi tempat wisata
    *   Category : Kategori tempat wisata
    *   City : Kota tempat wisata berada
    *   Price : Harga tempat wisata
    *   Rating : Rating tempat wisata
    *   Time_Minutes : Lama waktu berwisata
    *   Coordinate : Koordinat tempat wisata
    *   Lat : Latitude tempat wisata
    *   Long : Panjang dari tempat wisata
    *   Unamed: 11 : Data tanpa penjelasan
    *   Unamed: 12 : Data tanpa penjelasan
*   Variabel pada user.csv
    *   User_Id : Id dari user
    *   Location : Lokasi user
    *   Age : Umur user

**Data Understanding Collaborative Filtering**
- Menggunakan data preparation pada data preparation, buat variabel baru bernama cf dengan memasukkan data preparation.
- Kemudian encoder User_Id dan Place_Id menjadi indeks integer.
- Kemudian mapping User_Id dan Place_Id kedalam proses encoder sebelumnya.
- Kemudian cek jumlah user dan place, lalu ubah nilai Place_Ratings menjadi float
    
### Data Preprocessing

**Data Analysis**

- Menentukan file.csv yang akan digunakan untuk sistem rekomendasi, file yang digunakan diantaranya :
  - tourism_with_id.csv pada variabel tourism
  - tourism_rating.csv pada variabel rating
- Kemudian cek jumlah fitur numerik dan kategori pada tourism, diperoleh informasi numerik terdiri dari 8 fitur, dan kategori terdiri dari 5 fitur, diantaranya sebagai berikut :
  - Numerik :
    - Place_Id : int64
    - Price : int64
    - Rating : float64
    - Time_Minutes : float64
    - Lat : float64
    - Long : float64
    - Unnamed: 11 : float64
    - Unnamed: 12 : float 64
  - Kategori :
    - Place_Name : object
    - Description : object
    - Category : object
    - City : object
    - Coordinate : object 
- Karena pada sistem rekomendasi ini hanya merekomendasikan tempat wisata berdasarkan tempat wisata yang telah dikunjungi sebelumnya, maka fitur selain Place_Id, Place_Name dan Category akan dihapus.
- Kemudian cek jumlah fitur numerik dan kategori pada rating, diperoleh informasi numerik 3 fitur sedangkan kategori tidak ada, diantaranya sebagai berikut :
- Numerik :
  -  User_Id : int64
  -  Place_Id : int64
  -  Place_Ratings : int64
-  Kemudian melihat distribusi data dari rating

   |       |      User_Id |     Place_Id | Place_Ratings |
   |:-----:|-------------:|-------------:|--------------:|
   | count | 10000.000000 | 10000.000000 |  10000.000000 |
   |  mean |   151.292700 |   219.416400 |      3.066500 |
   |  std  |    86.137374 |   126.228335 |      1.379952 |
   |  min  |     1.000000 |     1.000000 |      1.000000 |
   |  25%  |    77.000000 |   108.750000 |      2.000000 |
   |  50%  |   151.000000 |   220.000000 |      3.000000 |
   |  75%  |   226.000000 |   329.000000 |      4.000000 |
   |  max  |   300.000000 |   437.000000 |      5.000000 |

   Terlihat pada tabel distribusi, dapat dipastikan tidak terdapat bahwa terdapat data duplikat pada fitur User_Id, data duplikat ini akan diproses pada proses data preparation.
- Kemudian menggabungkan fitur Category dan Place_Name pada tourism ke dalam variabel rating.
- Kemudian cek data null pada variabel all_tourism yang berisi fitur-fitur yang telah digabung sebelumnya.

**Univariate Exploratory Data Analysis**
- Melakukan teknik EDA menggunakan univariate analysis dengan memvisualisasikan data untuk memahami satu persatu data pada fitur yang telah diolah sebelumnya.
  - Fitur Place_Ratings
   
    ![image](https://user-images.githubusercontent.com/58927608/229636612-44a0cbc7-5628-4df6-91c0-4381a1559bca.png)
    
    Dapat dilihat pada visualisasi diatas, masing-masing rating memiliki persentase yang hampir mirip, berikut merupakan persentase dan jumlah sample secara spesifik dari visualisasi diatas diurutkan dari yang terbanyak hingga terendah :
    - Rating 4 : 2106 sample, 21.1%
    - Rating 3 : 2096 sample, 21.0%
    - Rating 2 : 2071 sample, 20.7%
    - Rating 5 : 2021 sample, 20.2%
    - Rating 1 : 1706 sample, 17.1%
  
  - Fitur Category
    
    ![image](https://user-images.githubusercontent.com/58927608/229637643-11ee4916-1d40-4fc4-b142-2592e1343635.png)
    
    Terlihat bahwa 50% dari keseluruhan data berada pada Category Taman Hiburan dan Budaya, berikut merupakan presentase dan jumlah sample spesifik dari fitur Category diurutkan dari terbesar hingga terendah :
    - Taman Hiburan : 3053 sample, 30.5%
    - Budaya : 2683 sample, 26.8%
    - Cagar Alam : 2415 sample, 24.2%
    - Bahari : 1079 sample, 10.8%
    - Pusat Perbelanjaan : 385 sample, 3.8%
    - Tempat Ibadah : 385 sample, 3.8%

  - Fitur Place_Name
    Untuk fitur Place_Name disini hanya menampilkan banyak tempat wisata. Diperoleh bahwa banyak tempat wisata yang akan digunakan untuk sistem rekomendasi adalah sebanyak 437.
  
## Data Preparation
Teknik Data preparation yang dilakukan terdiri dari:
 - Menghapus data duplikat pada Place_Id yang sudah ditunjukkan pada bagian Data Preprocessing
 - Membuat dictionary untuk data baru yang berisi fitur place_id, place_category dan place_name

**Proses Data Preparation**
- Cek apakah ada data null pada data all_tourism
- Kemudian cek banyak data pada all_tourism, diperoleh informasi bahwa banyak data sekarang adalah 437
- Setelah itu buat variabel baru preparation yang berisi data dari all_tourism
- Kemudian hapus nilai duplikat pada fitur Place_Id
- Membuat variabel baru untuk membuat dictianory, seperti berikut :
  - `place_id = preparation['Place_Id'].tolist()`
  - `place_category = preparation['Category'].tolist()`
  - `place_name = preparation['Place_Name'].tolist()`
- Kemudian menggabungkan variabel baru tersebut ke dalam tourism_recommend 

**Splitting Training & Validation Data untuk Collaborative Filtering**
- Lakukan distribusi data dengan random_state agar data menjadi acak.
- Lakukan mapping data User_Id dan Place_Id menjadi skala 0 sampai 1
- Kemudian split data train dan validation menjadi 80:20

**Mengapa perlu dilakukan data prepration?** 
- Untuk menghilangkan data duplikat, karena dapat menyebabkan bias pada data
- Dibuatnya tourism_recommend untuk menampung fitur-fitur yang hanya akan digunakan untuk rekomendasi

## Modeling

## Model Content Based Filtering - Berdasarkan data wisatawan atau turis yang telah berkunjung ke tempat serupa sebelumnya 

**TF-IDF Vectorizer**
- Sebelum mengembangkan sistem rekomendasi dengan content-based filtering, masukkan data preparation ke variabel baru yaitu data.
- Kemudian membuat sistem rekomendasi berdasarkan tempat wisata yang telah dikunjungi sebelummnya, menggunakan TF-IDF Vectorizer dengan fungsi `tfidfvectorizer()` dari sklearn. Tahap ini terdiri dari inisialisasi TfidfVectorizer, kemudian perhitungan idf pada place_name dan mapping array dari fitur index ke fitur nama.
- Lakukan fitting dan transformasi fitur place_name dalam bentuk matriks.
- Mengubah vektor tf-dif dalam bentuk matrix dengan `fungsi todense()`

**Cosine Similarity**
- Selanjutnya membuat dataframe untuk melihat tf-idf matrix dengan kolom berisi place_name dan baris place_category, ini digunakan untuk melihat korelasi antar place_name dengan category.
- Kemudian menghitung derajat kesamaan (similarity degree) antar place_name menggunakan cosine_similarity dari sklearn.

**Mendapatkan Rekomendasi Destinasi Wisata**
- Membuat fungi tourism_recommendations dengan parameter sebagai berikut : 
  - nama_tempat : nama tempat wisata
  - similarity_data : dataframe similarity sebelumnya
  - items : fitur untuk mendefinisikan kemiripan dari plaec_name dan place_category
  - k : banyak rekomendasi yang diberikan
- Kemudian menemukan rekomendasi yang mirip dengan Pantai Baron, berikut merupakan output yang dihasilkan :
 
  |   |       place_name | place_category |
  |--:|-----------------:|---------------:|
  | 0 |     Pantai Ancol |         Bahari |
  | 1 |    Pantai Marina |         Bahari |
  | 2 |    Pantai Congot |         Bahari |
  | 3 |     Pantai Drini |         Bahari |
  | 4 | Pantai Ngrenehan |         Bahari |

**Kelebihan dan kekurangan *content-based filtering***

- Kelebihan *content-based filtering*
  - Kemapuan untuk merekomendasikan item yang bersifat personal dan baru bagi user

- Kekurangan *content-based filtering*
  - Terbatas pada rekomendasi pad item-item yang mirip sehingga tidak ada kesempatan untuk mendapatkan item yang diluar kemiripan

**Mengapa menggunakan *content-based filtering?***
- Karena sistem rekomendasi ini menampilkan rekomendasi berdasarkan tempat wisata yang telah dikunjungi pada wisatawan atau turis sebelumnya, sehingga menampilkan rekomendasi yang mirip pada wisata sebelumnya.

## Model Collaboratieve Filtering - Berdasarkan data rating wisatawan atau turis untuk merekomendasikan tempat bagi user untuk tempat yang tidak pernah dikunjungi 

**Training**
- Pada proses ini menghitung skor kecocokan wisatawan atau turis dengan destinasi wisata dengan teknik embedding.
- Membuat class RecommenderNet dengan keras Model class.
- Menginisialisasikan fungsi embedding.
- Membuat layer embedding user dan layer embedding user dengan bias, yang terdiri dari parameter sebagai berikut :
  - `num_users` : merupakan hasil encoder User_Id dalam indeks integer.
  - `embedding_size` : merupakan besaran dimensi vector yang digunakan untuk embedding
  - `embedding_initializer = 'he_normal'` : Inisialisasi untuk matrik embedding, disini menggunakan 'he_normal'
  - `embedding_regularizer = keras.regularizers.12(1e06)` : Fungsi regularizer yang diterapkan pada matrik embedding, disini menggunakan keras.regularizers.12(1e06)
- Membuat layer embedding place dan layer embedding place dengan bias, yang terdiri dari parameter sebagai berikut :
  - `num_places` : merupakan hasil encoder Places_Id dalam indeks integer.
  - `embedding_size` : merupakan besaran dimensi vector yang digunakan untuk embedding
  - `embedding_initializer = 'he_normal'` : Inisialisasi untuk matrik embedding, disini menggunakan 'he_normal'
  - `embedding_regularizer = keras.regularizers.12(1e06)` : Fungsi regularizer yang diterapkan pada matrik embedding, disini menggunakan keras.regularizers.12(1e06)
- Membuat fungsi call yang memanggil layer embedding 1,2,3, dan 4.
- Kemudian menggunakan activation sigmoid.
- Lakukan compile pada model yang telah dibuat dengan loss `BinaryCrossentropy()`, optimizer `Adam()` dengan `learning_rate = 0.001`, dan metrics `RootMeanSquaredError()`.
- Lakukan proses training dengan `batch_size = 8` dan `epochs = 100`.

**Mendapatkan Rekomendasi Destinasi Wisata**
- Agar mendapatkan rekomendasi destinasi wisata, sebaiknya acak sample yang didefinisikan pada places_not_visited menggunakan operator bitwise (~) yang diperoleh pada variabel places_visited_by_user.
- Kemudian untuk memperoleh rekomendasi destinasi wisata, gunakan model.predict(), berikut merupakan output rekomendasi yang dihasilkan :

  Showing recommendations for users : 41
  
  **Place with high ratings from user**
  
  |                 Place_Name |      Category |
  |---------------------------:|--------------:|
  |     Flower Farm Setiya Aji |    Cagar Alam |
  |         Candi Gedong Songo |        Budaya |
  |                   Goa Rong |    Cagar Alam |
  | Pemandian Air Panas Ciater |    Cagar Alam |
  |                Taman Mundu | Taman Hiburan |
  
  **Top 10 place recommendation**
  
  |                          Place_Name |           Category |
  |------------------------------------:|-------------------:|
  |                  Kebun Teh Nglinggo |         Cagar Alam |
  |                   Desa Wisata Kelor |      Taman Hiburan |
  |           Seribu Batu Songgo Langit |         Cagar Alam |
  | Desa Wisata Rumah Domes/Teletubbies |      Taman Hiburan |
  |                 Wisata Kraton Jogja |             Budaya |
  |      Grojogan Watu Purbo Bangunrejo |      Taman Hiburan |
  |         Kawasan Wisata Sosrowijayan | Pusat Perbelanjaan |
  |                        Pantai Baron |             Bahari |
  |                     Pantai Ngobaran |             Bahari |
  |                       Bendung Lepen |      Taman Hiburan |

**Kelebihan dan kekurangan *Collaborative Filtering***

- Kelebihan *Collaborative Filtering*
  - Rekomendasi akan tetap bekerja dalam keadaan dimana konten sulit dianalisa.

- Kekurangan *Collaborative Filtering*
  -  Membutuhkan parameter rating, sehingga jika ada item baru dalam sistem maka tidak akan direkomendasikan.

**Mengapa menggunakan model tersebut?**
- Karena sistem rekomendasi ini menampilkan rekomendasi berdasarkan rating, dimana tujuan dari collaborative filtering adalah untuk merekomendasikan destinasi wisata walaupun wisatawan atau turis tidak pernah pergi kesuatu tempat destinasi wisata sebelumnya.

## Evaluation

## Evaluasi Content Based Filtering

- Metrik evaluasi yang digunakan adalah recommender system precision. Disini precision merupakan jumlah item yang direkomendasikan yang relevan.
**Formula Mean Squared Error dan cara Mean Squared Error bekerja**
Rumus yang digunakan untuk recommender system precision sebagai berikut :

  ![image](https://user-images.githubusercontent.com/58927608/229649814-1d36551c-687b-4118-b4df-a6f100433bb3.png)

**Bagaimana cara Mean Squared Error bekerja?**

Cara kerjanya adalah dengan membagi nilai item yang relevan dengan nilai jumlah item yang direkomendasikan, misalnya berikut

  |   |       place_name | place_category |
  |--:|-----------------:|---------------:|
  | 0 |     Pantai Ancol |         Bahari |
  | 1 |    Pantai Marina |         Bahari |
  | 2 |    Pantai Congot |         Bahari |
  | 3 |     Pantai Drini |         Bahari |
  | 4 | Pantai Ngrenehan |         Bahari |

Fitur yang relevan pada tabel diatas adalah 5 dengan jumlah total top-N adalah 5, apabila dimasukkan kedalam rumus maka akan menjadi seperti berikut :
 releven/jumlah item rekomendasi = 5/5 = 1 berarti precisionnya adalah 100%
 
## Evaluasi Collaborative Filtering

- Metrik evaluasi yang digunakan adalah Root Mean Squared Error (RMSE) yang mengukur tingkat akurasi hasil dari perkiraan model yang telah dibuat.
- Hasil yang diperoleh dari metrik ini sebagai berikut :
  
  ![image](https://user-images.githubusercontent.com/58927608/229677006-17ee8370-50ec-460c-98e6-ef8a7a0abde7.png)
  
  Dapat disumpulkan pada proses training nilai error akhir untuk training berada pada angka 0.29 dan error pada test pada angka 0.31. Sehingga nilai tersebut sudah cukup bagus untuk sistem rekomendasi `collaborative filtering`.

**Formula Mean Squared Error dan cara Mean Squared Error bekerja**

Rumus yang digunakan untuk RMSE sebagai berikut :

![image](https://user-images.githubusercontent.com/58927608/229663230-ae205eec-1cfa-4042-9e66-47714a4deb05.png)

**Bagaimana cara Mean Squared Error bekerja?**

Cara kerja RMSE adalah dengan mengkuadratkan error (prediksi '' observasi) kemudian dibagi dengan jumlah data (= rata-rata), kemudian hasil tersebut diakarkan.

REFERENSI :
  
  [PENGARUH SEKTOR PARAWISATA TEHADAP PERTUMBUHAN EKONOMI DI INDONESIA](https://repository.unair.ac.id/86231/1/TE.%2005-19%20Yak%20p%20ABSTRAK.pdf)
  
  [KONTRIBUSI PARIWISATA TERHADAP PENINGKATAN KESEJAHTERAAN
MASYARAKAT INDONESIA](http://jurnal.unpad.ac.id/prosiding/article/viewFile/13622/6452)

  [TOURISM EFFECT ON ECONOMIC
GROWTH IN INDONESIA](https://mpra.ub.uni-muenchen.de/65628/1/MPRA_paper_65628.pdf)

