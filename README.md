# **Laporan Proyek Machine Learning Terapan | Sistem Rekomendasi Judul Anime**
###### **Dibuat Oleh : Nisrina Fatimah Parisya**
---
![image](https://github.com/user-attachments/assets/cde4d32e-82b7-41ab-8b42-2ac992d42be7)

---
## **1. Domain Proyek**
### Latar Belakang
Pada era digital ini industri hiburan sangat beragam terutama dengan kehadiran platform streaming yang mempermudah akses masyarakat dalam mendapatkan hiburan berupa tontonan film, serial dan banyak jenis konten lainnya. Industri Anime yang berasal dari Jepang mengalami pertumbuhan yang pesat dengan berbagai jenis genre yang disajikan. Di Indonesia sendiri Anime sudah menjadi populer sejak tahun 1970-an, hal ini menyebabkan banyaknya pilihan bagi penonton sehingga kesulitan menemukan anime yang sesuai dengan preferensi dan selera mereka di antara puluhan ribu judul yang tersedia di platform streaming. Tantangan ini tidak hanya dialami oleh penonton casual, tetapi juga oleh anime enthusiast dan komunitas otaku yang membutuhkan rekomendasi personal untuk mengeksplorasi genre baru dan menemukan hidden gems dalam dunia anime yang sangat luas dan beragam.

Salah satu solusi untuk mengatasi masalah ini adalah penerapan sistem rekomendasi anime. Sistem ini dirancang untuk membantu penonton menemukan anime yang relevan secara efisien dan personal berdasarkan riwayat tontonan dan preferensi genre mereka. Pendekatan yang banyak digunakan adalah content-based filtering, yakni metode yang merekomendasikan anime berdasarkan kemiripan konten seperti genre, studio, tahun rilis, dan rating dengan anime-anime yang sebelumnya ditonton atau disukai pengguna. Algoritma seperti TF-IDF dan cosine similarity sering digunakan untuk mengukur tingkat kemiripan antar anime berdasarkan representasi numerik dari fitur-fitur tersebut. Penelitian menunjukkan bahwa pendekatan ini mampu menghasilkan rekomendasi dengan tingkat akurasi tinggi, mencapai hingga 85,6% dalam studi kasus rekomendasi anime berdasarkan kesamaan genre.

Penerapan sistem rekomendasi tidak hanya meningkatkan kepuasan dan engagement penonton dalam mengeksplorasi konten anime, tetapi juga berkontribusi terhadap peningkatan watch time dan subscriber retention pada platform streaming anime, serta membantu promosi anime-anime baru atau kurang populer kepada target audience yang tepat.

Manfaat untuk Pengguna/Penonton:
- Menghemat waktu dalam mencari anime yang sesuai preferensi di antara puluhan ribu judul
- Mendapatkan rekomendasi yang disesuaikan dengan selera dan riwayat tontonan pribadi
- Membantu penonton menemukan genre anime baru yang mungkin disukai
- Mengungkap anime berkualitas yang kurang populer atau terlewatkan

Manfaat untuk Platform Streaming:
- Penonton menghabiskan lebih banyak waktu menonton karena mendapat rekomendasi relevan
- Mempertahankan pelanggan dengan memberikan pengalaman yang lebih memuaskan
- Meningkatkan interaksi dan aktivitas pengguna di platform
- Membantu promosi konten baru atau kurang populer ke target audience yang tepat

Manfaat untuk Industri Anime:
- Membantu anime baru atau kurang dikenal mendapat exposure yang lebih baik
- Memberikan insights tentang preferensi penonton untuk pengembangan konten masa depan
- Meningkatkan konsumsi konten yang pada akhirnya berdampak pada pendapatan

## **2. Business Understanding**
### Problem Statements
1. Penonton anime menghadapi kesulitan dalam menemukan anime yang sesuai dengan preferensi mereka di antara puluhan ribu judul yang tersedia di platform streaming.
2. Penonton membutuhkan waktu yang lama untuk mengeksplorasi dan menemukan anime baru yang sesuai dengan selera mereka.

### Goals:
1. Membangun sistem rekomendasi anime berbasis content-based filtering yang dapat memberikan rekomendasi akurat berdasarkan kesamaan genre.
2. Mempercepat proses penemuan anime yang sesuai preferensi pengguna dengan rekomendasi yang personal dan relevan dengan menerapkan algoritma TF-IDF dan Cosine Similarity untuk mengukur kesamaan antar anime berdasarkan representasi numerik genre.

### Solution Statements:
1. Mengimplementasikan TF-IDF Vectorizer untuk mengubah data genre anime menjadi representasi numerik yang dapat diproses oleh algoritma machine learning.
2. Menggunakan cosine similarity untuk menghitung tingkat kesamaan antar anime berdasarkan vector representasi genre mereka.
3. Membangun sistem rekomendasi berbasis konten yang menganalisis kesamaan genre untuk memberikan rekomendasi yang relevan.
4. Mengembangkan fungsi get_anime_recommendations() yang dapat memberikan top-N rekomendasi anime berdasarkan input anime tertentu dengan similarity score yang transparan.
5. Mengimplementasikan sistem evaluasi yang mengukur Genre Similarity Average untuk memvalidasi kualitas rekomendasi yang dihasilkan.

## **3. Data Understanding**
Dataset yang digunakan merupakan dataset berjudul "Anime Data"  yang dapat diakses melalui kaggle dengan link berikut ini [Anime Data](https://www.kaggle.com/datasets/canggih/anime-data-score-staff-synopsis-and-genre). Dataset ini terdiri dari 1563 Baris dengan berisi judul-judul anime beserta variabel pendukung yang relevan, sehingga cocok untuk memberikan rekomendasi judul anime sejenis berdasarkan genre yang disukai pengguna.

**Kondisi Data**
* Ada kolom bertipe objek seperti:
`Title, Type, Episodes, Status, Start airing, End airing, Starting season, Broadcast time, Producers, Licensors, Studios, Sources, Genres, Duration, Rating, Score, Scored by, Members, Favorites, Description.`
* Ada juga kolom bertipe numerik:
`Score (float64), dan Scored by, Members, Favorites (int64).`
* Tidak ditemukan duplicate data pada 1563 baris dan 20 kolom data.
* Terdapat missing value pada kolom Rating sebanyak 9 baris

**Fitur yang terdapat pada setiap kolom dataset**:
 
| Kolom             | Deskripsi                                                                                        |
|-------------------|--------------------------------------------------------------------------------------------------|
| Title             | Nama resmi anime sebagai identitas utama                                                       |
| Type              | Jenis format anime seperti TV, Movie, OVA, dll                                                   |
| Episodes          | Jumlah total episode dalam anime tersebut                                                          |
| Status            | Status penayangan anime saat ini (selesai, tayang, atau belum)                                    |
| Start airing      | Tanggal mulai anime ditayangkan                                                                      |
| End airing        | Tanggal anime selesai tayang                                                                         |
| Starting season   | Musim dan tahun saat anime mulai tayang                                                             |
| Broadcast time    | Waktu penayangan anime di TV                                                                         |
| Producers         | Perusahaan atau pihak yang memproduksi anime                                                         |
| Licensors         | Pihak yang memegang lisensi tayang anime di luar Jepang                                                   |
| Studios           | Studio animasi yang membuat anime tersebut                                                             |

Pada fitur fitur dalam dataset Anime Data terdapat 16 Kolom bertipe data object (Data Kategorikal), 1 Kolom bertipe data float dan 3 kolom bertipe data integer (Data Numerikal).

### Exploratory Data Analysis (EDA)
#### Cek Ukuran Data
Tahapan ini dilakukan untuk memahami isi dataset. hal pertama yang dilakukan adalah memahami dan mengecek isi dari dataset dengan menggunakan `.shape', .info() `dan `.describe()`
![image](https://github.com/user-attachments/assets/f70f8ed0-cae4-40d2-8541-6ab377bcf2ff)

##### Cek Informasi Data
Dalam Cell dibawah ini dapat kita ketahui bahwa dataset terdiri dari 1563 barus data dengan 20 kolom

![image](https://github.com/user-attachments/assets/30b8b203-33f7-4401-998d-8269d5304896)

```
df.info()
```
Berdasarkan output tersebut kita dapat mengetahui ada beberapa jenis data:

* 16 Kolom dengan tipe data object yang termasuk dalam kategori kategorikal atau teks, contohnya: Title, Type, Status, Start airing, Genres, Studios, Description, dll.
Kolom-kolom ini berisi informasi non-numerik seperti judul anime, tipe (TV/Movie), studio produksi, atau deskripsi.

* 1 Kolom dengan tipe data float64 yang termasuk dalam kategori numerik, yaitu:
Score: nilai rating anime dalam bentuk desimal (contoh: 8.52)

* 3 Kolom dengan tipe data int64 yang juga termasuk kategori numerik, yaitu: Scored by, Members, dan Favorites, ketiganya menunjukkan jumlah vote, jumlah member, dan jumlah favorit dalam angka bulat.





