# Laporan Proyek Machine Learning - Moch. Yusuf Haidar Ali Ramdhani
# Proyek Sistem Rekomendasi

## Project Overview

Seiring perkembangan era digital, jumlah film yang tersedia secara daring melalui platform streaming seperti Netflix, Disney+, dan Amazon Prime Video meningkat secara signifikan. Hal ini memberikan kemudahan akses bagi pengguna, namun di sisi lain juga menimbulkan tantangan tersendiri—yakni kesulitan dalam memilih film yang sesuai dengan preferensi pribadi. Ketika dihadapkan pada ribuan pilihan, pengguna cenderung kebingungan dan membutuhkan bantuan sistem yang dapat menyaring pilihan tersebut secara efisien.

Sistem rekomendasi hadir sebagai solusi utama untuk mengatasi permasalahan ini. Menurut Ricci et al. (2010), sistem rekomendasi dirancang untuk menyarankan item yang paling relevan kepada pengguna berdasarkan riwayat interaksi atau preferensi mereka. Di dunia nyata, sistem ini menjadi komponen penting dalam meningkatkan pengalaman pengguna dan mempertahankan loyalitas, khususnya di industri hiburan digital. Tanpa sistem rekomendasi yang baik, pengguna berisiko kehilangan minat atau menghabiskan terlalu banyak waktu untuk mencari tontonan, yang pada akhirnya berdampak negatif pada tingkat keterlibatan (engagement) dan retensi pengguna.

Platform telah memungkinkan pengguna untuk memberikan rating atau ulasan terhadap film yang mereka tonton. Akan tetapi menurut Agustian et al. (2020), banyaknya jumlah user yang memberi review berbeda-beda pada suatu film membuat pembaca kebingungan dalam menyimpulkan review tersebut. Dengan demikian, pengembangan sistem rekomendasi yang cerdas dan personal menjadi sangat penting.

Proyek ini bertujuan untuk membangun sistem rekomendasi film dengan menggabungkan dua pendekatan utama, yaitu content-based filtering dan collaborative filtering berbasis model. Pendekatan content-based filtering akan memanfaatkan metadata film, seperti genre dan tahun, untuk merekomendasikan film yang mirip dengan film yang telah disukai pengguna. Di sisi lain, pendekatan collaborative filtering dengan teknik embedding akan menganalisis pola rating pengguna terhadap berbagai film untuk menangkap hubungan tersembunyi antar pengguna dan item. Metode ini dikembangkan menggunakan TensorFlow, dengan pemanfaatan embedding layer untuk menyandikan representasi pengguna dan film ke dalam ruang vektor laten.

Dengan menggabungkan kedua pendekatan tersebut, sistem rekomendasi yang dibangun dalam proyek ini diharapkan mampu memberikan hasil yang lebih akurat, relevan, dan sesuai dengan kebutuhan pengguna. Pendekatan hibrida ini memungkinkan sistem tidak hanya memahami kesukaan pengguna berdasarkan isi film, tetapi juga berdasarkan preferensi pengguna lain yang memiliki pola perilaku serupa.

**Referensi**

Agustian, E. R., Munir, & Nugroho, E. P. (2020). Sistem rekomendasi film menggunakan metode collaborative filtering dan K-nearest neighbors. JATIKOM: Jurnal Aplikasi dan Teori Ilmu Komputer, 3(1), 18–21.

Ricci, F., Rokach, L., & Shapira, B. (2010). Recommender Systems Handbook (pp. 1–35). https://doi.org/10.1007/978-0-387-85820-3_1

## Business Understanding

### Problem Statements

**1. Tingginya jumlah pilihan film menyebabkan pengguna mengalami kesulitan dalam menemukan tontonan yang sesuai preferensi pribadi.**

   Dengan ribuan judul film tersedia di platform digital, pengguna seringkali mengalami information overload sehingga memerlukan bantuan sistem yang mampu menyaring dan merekomendasikan film secara efisien.

**2. Sistem rekomendasi yang bersifat generik tidak mampu memberikan saran yang relevan secara personal.**

   Rekomendasi yang tidak mempertimbangkan pola perilaku unik dan preferensi spesifik pengguna berpotensi menghasilkan saran film yang tidak menarik, sehingga menurunkan kepuasan dan engagement pengguna.

### Goals

**1. Mengembangkan sistem rekomendasi film yang mampu mempersonalisasi saran tontonan berdasarkan preferensi pengguna.**
  
   Sistem ini dirancang untuk membantu pengguna menyaring ribuan film secara efisien dan menyarankan film yang paling relevan dengan selera mereka, sehingga mengurangi kebingungan dalam memilih.

**2. Meningkatkan relevansi rekomendasi melalui pemanfaatan data historis perilaku pengguna.**

   Sistem akan belajar dari pola penilaian dan interaksi pengguna untuk menghasilkan saran film yang sesuai dengan kebiasaan menonton masing-masing individu.

### Solution statements

**1. Content-Based Filtering**

Pendekatan ini memanfaatkan metadata film, seperti genre, untuk menghitung tingkat kemiripan antar film menggunakan teknik ekstraksi fitur seperti TF-IDF (Term Frequency-Inverse Document Frequency) dan pengukuran kesamaan menggunakan cosine similarity. Sistem kemudian merekomendasikan film yang memiliki kemiripan konten dengan film-film yang sebelumnya disukai oleh pengguna. Pendekatan ini sangat efektif untuk menangani masalah cold-start pada pengguna baru atau ketika data rating masih terbatas.

**2. Collaborative Filtering**

Metode ini membangun representasi vektor (embedding) untuk setiap pengguna dan film berdasarkan pola interaksi dan rating yang diberikan. Dengan menggunakan model neural network, seperti RecommenderNet yang dikembangkan menggunakan TensorFlow, sistem mempelajari hubungan kompleks antara pengguna dan film melalui embedding layer dan operasi dot product untuk memprediksi rating atau preferensi pengguna terhadap film yang belum pernah ditonton. Pendekatan ini memungkinkan rekomendasi yang lebih personal dan akurat dengan memanfaatkan data interaksi pengguna secara kolektif.

## Data Understanding

Dataset yang digunakan dalam proyek ini adalah Movie Recommendation System Dataset dari Kaggle, yang berbasis pada MovieLens dataset—sebuah dataset standar yang banyak digunakan untuk membangun dan mengevaluasi sistem rekomendasi film. Dataset ini tersedia secara publik dan dapat diakses di tautan berikut: https://www.kaggle.com/datasets/parasharmanas/movie-recommendation-system?select=ratings.csv

### Ringkasan Data:

- Jumlah film: Terdapat 9.742 data film.

- Jumlah rating: Terdapat 100.836 data rating.

Kondisi data: Data telah melalui proses pra-pemrosesan (preprocessing) dasar namun tetap memerlukan tahapan lanjutan seperti encoding, normalisasi, serta pembagian data untuk pelatihan dan validasi model.

### Variabel atau fitur penting dalam dataset movies adalah:

- movieId: Identifikasi unik setiap film.

- title: Judul film.

- genres: Kategori atau genre film, bisa lebih dari satu per film, dipisahkan dengan karakter tertentu.

- year (ditambahkan): tahun rilis film.

### Variabel atau fitur penting dalam dataset ratings adalah:

- userID: Identifikasi unik setiap pengguna.

- movieId: Identifikasi unik setiap film.

- rating: Nilai rating yang diberikan pengguna terhadap film (skala 0.5–5).

- timestamp: Waktu ketika rating diberikan.

### Insight

**Dataset Movies**

![info dataset](https://raw.githubusercontent.com/LapplandSa/Proyek-Sistem-Rekomendasi/main/images/movies.png)

Berdasarkan informasi struktur data, dataset movies.csv terdiri dari 9.742 entri dengan tiga kolom utama, yaitu movieId, title, dan genres. Seluruh data dalam ketiga kolom ini terisi penuh (tidak ada nilai yang hilang), yang menunjukkan kualitas data yang baik dari segi kelengkapan. Kolom movieId bertipe numerik dan digunakan sebagai pengenal unik untuk setiap film, sedangkan title dan genres bertipe objek (string). 

**Dataset Ratings**

![info dataset](https://raw.githubusercontent.com/LapplandSa/Proyek-Sistem-Rekomendasi/main/images/ratings.png)

Berdasarkan informasi struktur data, dataset ratings.csv terdiri dari 100.836 entri dengan empat kolom utama: userId, movieId, rating, dan timestamp. Semua kolom memiliki jumlah nilai yang lengkap tanpa missing value, yang menunjukkan bahwa data ini memiliki kualitas yang baik dan tidak memerlukan proses imputasi.

**Describe Ratings**

![Describe Ratings](https://raw.githubusercontent.com/LapplandSa/Proyek-Sistem-Rekomendasi/main/images/describe.png)

Berdasarkan hasil statistik deskriptif dari dataset ratings.csv, terdapat total 100.836 entri rating. Rata-rata rating yang diberikan pengguna adalah sekitar 3.50, dengan nilai minimum 0.5 dan maksimum 5.0, serta standar deviasi sebesar 1.04, yang menunjukkan bahwa pengguna cenderung memberikan rating yang cukup tinggi namun dengan variasi yang moderat.

Jumlah pengguna (userId) berkisar dari 1 hingga 610, yang mengindikasikan adanya 610 pengguna unik dalam dataset. Sementara itu, movieId memiliki rentang dari 1 hingga 193.609, meskipun tidak semua ID di antaranya merupakan film yang benar-benar ada—sebagian mungkin tidak tercantum dalam dataset movies.csv.

Kolom timestamp menunjukkan waktu rating dalam bentuk Unix time, dengan nilai yang berkisar dari sekitar tahun 1996 hingga 2018, memberikan peluang untuk melakukan analisis tren waktu.

**Visualisasi Kolom Genre**

![Visualisasi Kolom Genre](https://raw.githubusercontent.com/LapplandSa/Proyek-Sistem-Rekomendasi/main/images/genre.png)

Berdasarkan distribusi jumlah film per genre, dapat disimpulkan bahwa genre Drama merupakan yang paling dominan dalam dataset dengan total 4.359 film, diikuti oleh Comedy sebanyak 3.756 film. Genre-genre populer lain seperti Thriller, Action, dan Romance juga memiliki representasi yang signifikan.

Sementara itu, genre yang lebih spesifik atau niche seperti Film-Noir, Western, dan IMAX memiliki jumlah film yang relatif sedikit, masing-masing hanya di bawah 200 judul. Terdapat pula 25 film yang tidak memiliki informasi genre ((no genres listed)), yang kemungkinan perlu dipertimbangkan untuk dihapus atau ditangani secara khusus dalam proses analisis dan pemodelan.

**Visualisasi Rating**

![Visualisasi Rating](https://raw.githubusercontent.com/LapplandSa/Proyek-Sistem-Rekomendasi/main/images/rating.png)

Distribusi rating film dalam dataset menunjukkan bahwa sebagian besar pengguna memberikan penilaian yang berada di kisaran menengah hingga tinggi. Rating terbanyak adalah 4.0 dengan 26.809 entri, diikuti oleh rating 3.0 sebanyak 20.038 entri, dan rating 5.0 sebanyak 13.203 entri. Sementara itu, rating rendah seperti 0.5 dan 1.0 hanya diberikan masing-masing sebanyak 1.367 dan 2.809 kali. Pola ini mencerminkan kecenderungan pengguna untuk memberikan penilaian yang positif terhadap film yang mereka tonton, yang dapat menjadi indikasi bahwa data memiliki bias terhadap penilaian yang baik.

## Data Preparation

### Menangani Missing Value

Karena tidak ditemukan data yang hilang, tidak diperlukan tindakan pembersihan atau imputasi pada tahap ini. Dengan demikian, tidak diperlukan tindakan pembersihan atau imputasi pada tahap ini. Seluruh data dapat langsung digunakan untuk proses eksplorasi, pemodelan, dan pembuatan sistem rekomendasi. Menangani nilai yang hilang merupakan langkah penting dalam tahap data preparation, karena data yang tidak lengkap dapat menyebabkan kesalahan dalam analisis dan membuat model pembelajaran mesin menghasilkan prediksi yang tidak akurat.

### Menangani Data Duplikat

Dalam proses pembersihan data, ditemukan bahwa meskipun tidak terdapat data duplikat berdasarkan movieId, terdapat beberapa entri pada kolom title yang memiliki judul identik atau sangat mirip. Hal ini berpotensi menyebabkan sistem rekomendasi memberikan saran yang redundan dengan film yang terlihat sama. Untuk mengatasi hal tersebut, dilakukan proses data cleaning tambahan dengan mengelompokkan dan menghapus entri yang memiliki judul identik atau serupa.

### Menambahkan Kolom Year

Pada tahap ini, dilakukan ekstraksi tahun rilis film dari kolom title pada dataset movies. Informasi tahun rilis umumnya tercantum di dalam tanda kurung pada akhir judul film, misalnya "Toy Story (1995)". Dengan menggunakan teknik pemrosesan teks (regular expression), angka tahun empat digit berhasil diambil dan disimpan dalam kolom baru bernama year. Penambahan kolom ini bermanfaat dalam proses analisis lebih lanjut, seperti tren perilisan film, preferensi pengguna berdasarkan tahun, atau penyaringan rekomendasi berdasarkan dekade tertentu.

Setelah menambahkan kolom year dari informasi dalam title, ditemukan beberapa baris yang tidak memiliki nilai tahun rilis yang valid—umumnya karena format judul yang tidak konsisten atau tidak mencantumkan tahun. Untuk menjaga kualitas data dan menghindari potensi error dalam analisis maupun saat membangun sistem rekomendasi, baris-baris tersebut dihapus dari dataset.

### Mengecek Kolom Genre

Kolom genres pada dataset berisi informasi mengenai kategori atau jenis film, seperti Action, Comedy, Drama, dan sebagainya. Setiap film dapat memiliki satu atau lebih genre yang dipisahkan dengan tanda pipe (|). Selain itu, terdapat juga entri dengan genre 'no genres listed', yang menandakan bahwa informasi genre tidak tersedia untuk film tersebut.

Untuk menjaga konsistensi dan kualitas analisis, terutama dalam proses pemodelan berbasis konten (content-based filtering) yang sangat bergantung pada informasi genre, maka baris-baris dengan genre tidak tersedia dihapus. Langkah ini dilakukan agar setiap film yang direkomendasikan memiliki metadata yang lengkap dan relevan.

### Mengecek Dataset Ratings

Dataset ratings berisi informasi penilaian dari pengguna terhadap film. Terdapat empat kolom utama dalam dataset ini, yaitu userId, movieId, rating, dan timestamp. Setelah dilakukan pencocokan antara dataset ratings.csv dan movies.csv, ditemukan bahwa terdapat 38 movieId di ratings.csv yang tidak memiliki pasangan data film di movies.csv. Contoh movieId yang tidak ditemukan antara lain: 166024, 122888, 122896, 167570, 140956. Hal ini bisa terjadi karena perbedaan versi data atau ketidaksesuaian dalam proses penggabungan data. Untuk memastikan konsistensi dan menghindari error saat penggabungan (merge), seluruh baris di ratings.csv yang memiliki movieId tidak ditemukan di movies.csv telah dihapus.

Distribusi nilai rating berada pada rentang 0.5 hingga 5.0, dengan interval 0.5, yang mencerminkan tingkat kepuasan pengguna terhadap film. Nilai ini sangat penting dalam pendekatan collaborative filtering, di mana pola rating digunakan untuk mempelajari preferensi pengguna dan menghasilkan rekomendasi yang personal.

Sementara itu, kolom timestamp menyimpan informasi waktu kapan rating diberikan. Meskipun tidak selalu digunakan dalam model berbasis embedding, data ini dapat berguna untuk analisis tren atau segmentasi berdasarkan periode waktu tertentu.

### Content-Based Filtering

#### Text Preprocessing (pada metadata film)

Dalam tahap preprocessing metadata film, dilakukan beberapa transformasi terhadap informasi genre dan tahun rilis untuk memperkuat representasi konten yang akan digunakan dalam sistem rekomendasi berbasis Content-Based Filtering. Pertama, kolom year diubah menjadi tipe data string agar dapat digabungkan dengan informasi genre dalam satu representasi teks. Selanjutnya, kolom baru bernama genre_year dibentuk dengan menggabungkan informasi genres dan year pada setiap film. Tujuannya adalah untuk menciptakan fitur teks gabungan yang merepresentasikan karakteristik utama film dalam bentuk yang dapat dianalisis menggunakan teknik berbasis teks seperti TF-IDF.

Selain itu, dibuat juga kolom genre_year_boosted dengan menduplikasi informasi genre dalam string hasil gabungan. Pada kolom ini, genre disebutkan dua kali sebelum ditambahkan dengan tahun rilis film. Pendekatan ini bertujuan untuk meningkatkan bobot informasi genre dalam proses ekstraksi fitur selanjutnya, sehingga model akan lebih memprioritaskan kesamaan genre dibandingkan kesamaan tahun rilis. Teknik boosting semacam ini berguna dalam kasus di mana preferensi pengguna lebih dipengaruhi oleh kesamaan genre daripada faktor lain. Transformasi ini merupakan langkah penting dalam membangun model Content-Based Filtering yang lebih sensitif terhadap atribut-atribut konten yang relevan.

#### TF-IDF Vectorization (Feature Extraction)

Setelah representasi teks genre_year_boosted berhasil dibuat pada tahap preprocessing, langkah selanjutnya adalah mengubah teks tersebut menjadi bentuk numerik agar dapat digunakan dalam sistem rekomendasi berbasis konten (Content-Based Filtering). Proses ini dilakukan dengan menggunakan teknik TF-IDF (Term Frequency–Inverse Document Frequency), yang berfungsi untuk memberikan bobot pada setiap kata berdasarkan frekuensinya dalam dokumen tertentu relatif terhadap seluruh dokumen dalam korpus. Dalam konteks ini, setiap film diperlakukan sebagai sebuah dokumen, dan nilai TF-IDF dihitung berdasarkan kolom genre_year_boosted yang menggabungkan genre (dengan boosting) dan tahun rilis.

TF-IDF memberikan penekanan lebih pada genre karena informasi genre diduplikasi dua kali dalam string input, sesuai dengan strategi boosting yang diterapkan sebelumnya. Hal ini membuat sistem lebih peka terhadap kesamaan genre saat melakukan pencocokan antar film.

Inisialisasi TfidfVectorizer dilakukan dengan parameter token_pattern=r'[^| ]+', agar dapat memisahkan token berdasarkan karakter pemisah seperti tanda | dan spasi, yang umum digunakan dalam format genre. Proses fit_transform menghasilkan matriks TF-IDF (tfidf_matrix) yang merepresentasikan setiap film sebagai vektor berdimensi sejumlah token unik dalam seluruh korpus genre_year_boosted.

Untuk keperluan interpretasi dan debugging, matriks ini kemudian dikonversi menjadi sebuah DataFrame (tfidf_df) dengan indeks berupa judul film dan kolom-kolom yang mewakili setiap token yang diekstrak. Matriks TF-IDF inilah yang akan menjadi dasar perhitungan kesamaan antar film menggunakan cosine similarity pada tahap berikutnya dalam sistem Content-Based Filtering.

### Collaborative Filtering

#### Encoding/Mapping

Dalam sistem rekomendasi berbasis kolaboratif, model memerlukan input dalam bentuk numerik terstruktur, terutama untuk entitas diskret seperti userId dan movieId. Oleh karena itu, dilakukan proses encoding, yaitu mengubah nilai-nilai userId dan movieId asli menjadi indeks numerik berurutan. Proses ini dilakukan dengan membangun dua buah kamus pemetaan: user_to_user_encoded untuk memetakan userId ke indeks, dan movie_to_movie_encoded untuk movieId. Kebalikannya, user_encoded_to_user dan movie_encoded_to_movie digunakan untuk mengubah kembali dari indeks ke ID asli jika diperlukan.

Setelah kamus pemetaan dibuat, kolom userId dan movieId pada DataFrame ratings kemudian dipetakan ke kolom baru user dan movie yang berisi hasil encoding. Proses ini penting agar data dapat digunakan dalam model embedding yang mengasumsikan entitas dikodekan sebagai indeks integer dari 0 hingga N.

#### Normalisasi Rating

Sebelum digunakan dalam proses pelatihan model, kolom rating perlu dinormalisasi dan dikonversi ke tipe data yang sesuai. Pada tahap ini, semua nilai pada kolom rating diubah menjadi tipe float32 untuk efisiensi komputasi dan kompatibilitas dengan TensorFlow. Selain itu, meskipun belum dilakukan normalisasi skala langsung dalam kode ini, model yang digunakan meng-output nilai dalam rentang [0, 1] akibat penggunaan fungsi aktivasi sigmoid. Oleh karena itu, selama pelatihan model, nilai rating akan dinormalisasi secara eksplisit (dalam proses model.fit) dengan membagi nilai rating aktual dengan 5, agar berada pada skala yang sama dengan output model.

Informasi tambahan seperti jumlah total pengguna (num_users), jumlah total film (num_movies), dan rentang rating (minimum hingga maksimum) juga dicetak untuk memberikan konteks terhadap skala data dan memverifikasi integritas preprocessing sebelum digunakan lebih lanjut.

#### Data Splitting

Setelah seluruh data telah melalui proses encoding dan normalisasi, langkah selanjutnya adalah membagi data ke dalam dua subset: data latih (train) dan data uji (test). Pembagian ini bertujuan untuk mengukur kemampuan generalisasi model terhadap data yang belum pernah dilihat sebelumnya.

Proses pembagian dilakukan menggunakan fungsi train_test_split dari library scikit-learn, dengan proporsi 80% data digunakan untuk pelatihan dan 20% sisanya untuk pengujian. Parameter random_state=42 digunakan untuk memastikan bahwa hasil pembagian bersifat reproducible, sehingga eksperimen dapat diulang dengan hasil yang konsisten. Pembagian dilakukan tanpa stratifikasi karena data merupakan interaksi user-item yang bersifat numerik dan kontinu, sehingga tidak memiliki label kelas yang perlu dipertahankan distribusinya.

Setelah pembagian, bentuk (shape) dari masing-masing subset dicetak sebagai verifikasi akhir, memastikan bahwa data telah berhasil dipisahkan dan siap digunakan dalam proses pelatihan dan evaluasi model rekomendasi.

#### Feature dan Label Separation

Setelah data pelatihan dan pengujian dipersiapkan, langkah selanjutnya adalah memisahkan fitur (input) dan label (target) yang akan digunakan dalam proses pelatihan model. Fitur yang digunakan terdiri dari pasangan (user, movie) yang telah melalui proses encoding sebelumnya. Sementara itu, label yang menjadi target prediksi adalah nilai rating dari setiap interaksi pengguna terhadap film.

Untuk memisahkan data tersebut, digunakan slicing terhadap kolom-kolom pada DataFrame train dan test. Kolom user dan movie disatukan menjadi variabel x_train dan x_test sebagai fitur input, sedangkan kolom rating diambil sebagai y_train dan y_test sebagai label target. Pemisahan ini penting untuk memastikan bahwa model hanya menerima informasi yang dibutuhkan untuk melakukan prediksi terhadap rating berdasarkan kombinasi pengguna dan film tertentu.

## Modeling

Pada tahap ini, dibangun dua model sistem rekomendasi menggunakan pendekatan yang berbeda: Content-Based Filtering dan Collaborative Filtering berbasis model Neural Network. Pendekatan ini dipilih untuk saling melengkapi dalam memberikan rekomendasi yang lebih relevan dan akurat kepada pengguna.

### Content-Based Filtering

Pendekatan Content-Based Filtering pada sistem rekomendasi ini dibangun dengan memanfaatkan metadata film, khususnya kolom genres dan year. Setelah dilakukan preprocessing dan penggabungan informasi tersebut ke dalam satu kolom genre_year_boosted, dilakukan ekstraksi fitur menggunakan metode TF-IDF (Term Frequency–Inverse Document Frequency). TF-IDF membantu merepresentasikan setiap film sebagai vektor berdasarkan kata-kata yang muncul di genre dan tahun rilisnya, sehingga film dengan genre serupa memiliki representasi vektor yang lebih mirip.

Setelah vektorisasi selesai, dihitung kemiripan antar film menggunakan cosine similarity, yang direpresentasikan dalam bentuk matriks. Kemiripan ini dihitung menggunakan fungsi linear_kernel dari sklearn.metrics.pairwise, yang secara efisien menghasilkan skor kemiripan antara seluruh pasangan film dalam bentuk matriks simetri.

Untuk memberikan rekomendasi, dikembangkan sebuah fungsi recommend(title, top_n=10) yang menerima masukan judul film dan mengembalikan daftar film lain yang paling mirip. Fungsi ini bekerja dengan mengambil indeks film yang diminta, mencari skor kemiripan tertinggi terhadap film lain (kecuali dirinya sendiri), dan mengembalikan top-N film berdasarkan nilai kemiripan tertinggi. Hasil rekomendasi berupa informasi judul, genre, dan tahun rilis dari film-film yang dianggap paling relevan dengan input pengguna.

**Langkah-langkah:**

- Kolom genres dan year digabung menjadi satu fitur teks untuk mewakili konten film.

- Fitur tersebut diproses menggunakan TF-IDF Vectorizer, yang mengubah teks menjadi vektor numerik berdasarkan frekuensi dan kekhasan kata dalam dokumen.

- Dihitung cosine similarity antar film berdasarkan representasi vektor TF-IDF.

- Untuk pengguna tertentu, sistem mengidentifikasi film-film yang telah mereka beri rating tinggi, lalu mencari film lain dengan kemiripan tertinggi terhadap film-film tersebut.

- Sistem menghasilkan top-N rekomendasi berdasarkan skor kemiripan tertinggi.

**Output:**

![Result](https://raw.githubusercontent.com/LapplandSa/Proyek-Sistem-Rekomendasi/main/images/result1.png)

Sistem rekomendasi berbasis konten yang dikembangkan dalam proyek ini bertujuan merekomendasikan film kepada pengguna berdasarkan kesamaan atribut kontennya, dalam hal ini adalah genre film. Sebagai studi kasus, film Toy Story digunakan sebagai acuan karena memiliki genre yang cukup khas, yaitu Adventure|Animation|Children|Comedy|Fantasy.

Berdasarkan hasil pemodelan menggunakan TF-IDF pada kombinasi genre, sistem mampu menghasilkan daftar rekomendasi yang sangat relevan. Sepuluh film teratas yang direkomendasikan seluruhnya memiliki genre yang identik dengan film acuan, meskipun tahun rilisnya bervariasi. Di antaranya terdapat film populer seperti Monsters, Inc., Shrek the Third, Toy Story 2, dan Antz, yang memang dikenal memiliki tema dan gaya serupa dengan Toy Story. Ini menunjukkan bahwa sistem berhasil mengidentifikasi pola genre yang kompleks dan menggunakannya untuk memberikan saran film yang konsisten secara tematik.

Rekomendasi yang konsisten ini mencerminkan bahwa model memiliki kemampuan mengenali genre sebagai fitur utama dalam menentukan kemiripan film. Hal ini juga memperkuat potensi sistem untuk digunakan pada skenario cold-start, di mana informasi historis pengguna belum tersedia, tetapi preferensi dapat disimpulkan dari satu atau beberapa film yang diketahui disukai.

**Kelebihan:**

- Efektif untuk menghadapi cold start pada pengguna baru karena tidak memerlukan data perilaku pengguna lain.

- Rekomendasi dapat dijelaskan secara eksplisit berdasarkan atribut film (misalnya genre).

**Kekurangan:**

- Sangat bergantung pada kualitas dan kelengkapan metadata film.

- Tidak memanfaatkan pola preferensi kolektif dari komunitas pengguna, sehingga bisa kehilangan konteks sosial.

### Collaborative Filtering Berbasis Model (Neural Network)

Model Collaborative Filtering dalam proyek ini dibangun menggunakan pendekatan Deep Learning, di mana relasi antara pengguna dan film direpresentasikan dalam bentuk embedding. Model ini bertujuan untuk mempelajari preferensi pengguna berdasarkan interaksinya dengan berbagai film, tanpa memanfaatkan metadata konten film secara eksplisit.

**Arsitektur Model**

Model dikembangkan dalam bentuk kelas RecommenderNet, yang merupakan subclass dari tf.keras.Model. Di dalamnya terdapat dua embedding utama:

- User Embedding: Menyandikan representasi vektor untuk setiap pengguna berdasarkan indeks user.

- Movie Embedding: Menyandikan representasi vektor untuk setiap film berdasarkan indeks movie.

Masing-masing embedding memiliki ukuran vektor sebesar 50 dimensi, yang dipilih sebagai hyperparameter embedding_size. Selain vektor embedding, model juga menyertakan bias term untuk pengguna dan film dalam bentuk layer Embedding tambahan.

Pada saat inferensi, model menghitung produk dot (dot product) antara vektor user dan vektor movie, kemudian menambahkan bias user dan movie. Hasil akhirnya diproses melalui fungsi aktivasi sigmoid sehingga nilai output berada dalam rentang 0 hingga 1. Karena rating asli berada pada skala 0–5, target output distandarisasi ke dalam rentang 0–1 dengan cara membagi nilai rating dengan 5 selama pelatihan.

**Proses Pelatihan**

Model dikompilasi dengan menggunakan fungsi loss Mean Squared Error (MSE), karena tugas utama adalah regresi nilai rating. Optimizer yang digunakan adalah Adam dengan learning rate sebesar 0.001. Selama pelatihan, metrik evaluasi yang dipantau adalah Root Mean Squared Error (RMSE).

Model dilatih selama 10 epoch dengan ukuran batch sebesar 64, dan divalidasi terhadap set data pengujian. Data pelatihan dan pengujian merupakan hasil dari proses split sebesar 80:20 dari dataset awal, di mana fitur user dan movie digunakan sebagai input, dan kolom rating digunakan sebagai target.

Pendekatan ini mampu menangkap pola kolaboratif antara pengguna dan item, sehingga menghasilkan rekomendasi berdasarkan perilaku pengguna lain yang mirip, meskipun tidak memiliki informasi eksplisit tentang genre atau tahun film.

**Langkah-langkah:**

- Dibangun model RecommenderNet dengan TensorFlow, terdiri dari dua embedding layer (untuk user dan item), dilanjutkan dengan dot product.

- Input berupa pasangan userId dan movieId.

- Target adalah rating aktual pengguna terhadap film.

- Setelah pelatihan, sistem memprediksi rating dari semua film yang belum ditonton oleh pengguna, kemudian mengurutkan berdasarkan nilai prediksi tertinggi.

**Output:**

![Result](https://raw.githubusercontent.com/LapplandSa/Proyek-Sistem-Rekomendasi/main/images/result2.png)

Sistem rekomendasi berbasis Collaborative Filtering yang telah dikembangkan berhasil menghasilkan daftar film yang dipersonalisasi untuk pengguna dengan ID 1. Berdasarkan hasil prediksi rating dari model, lima film teratas yang direkomendasikan kepada pengguna ini menunjukkan skor prediksi yang sangat tinggi, menandakan kecocokan preferensi yang kuat antara pengguna dan film-film tersebut.

Film dengan prediksi tertinggi adalah The Usual Suspects, dengan skor prediksi sebesar 4.77, diikuti oleh Star Wars: Episode IV - A New Hope (4.76), dan Forrest Gump (4.75). Dua film berikutnya dalam daftar adalah The Princess Bride dan Raiders of the Lost Ark, masing-masing dengan skor prediksi 4.75 dan 4.74. Seluruh film ini termasuk dalam kategori film populer dengan nilai artistik dan naratif yang tinggi, yang umum disukai oleh banyak penonton.

Rekomendasi ini menunjukkan bahwa model mampu mengidentifikasi pola preferensi pengguna berdasarkan interaksi historis pengguna-pengguna lain yang serupa. Dengan pendekatan ini, sistem dapat memberikan saran film yang lebih bersifat personal dan relevan, bahkan tanpa perlu mengetahui detail konten film secara langsung. Keberhasilan model dalam menyarankan film-film berkualitas tinggi juga menjadi indikator bahwa pemodelan dan pelatihan telah dilakukan secara efektif.

**Kelebihan:**

- Mampu menangkap pola kompleks antara pengguna dan item.

- Rekomendasi bersifat personalized berdasarkan preferensi pengguna.

**Kekurangan:**

- Membutuhkan cukup banyak data rating agar dapat belajar representasi dengan baik.

- Tidak dapat bekerja optimal pada pengguna baru (cold start problem).

## Evaluation

### Evaluation untuk Content-Based Filtering

Evaluasi pada sistem rekomendasi berbasis konten (Content-Based Filtering) dilakukan dengan menghitung metrik Precision@10, yang mengukur seberapa relevan rekomendasi yang diberikan terhadap preferensi pengguna. Dalam konteks ini, relevansi didefinisikan sebagai film yang memiliki genre yang sama persis dengan film yang menjadi input (dalam hal ini, Toy Story dengan genre: Adventure|Animation|Children|Comedy|Fantasy).

![Precision](https://raw.githubusercontent.com/LapplandSa/Proyek-Sistem-Rekomendasi/main/images/result6.png)

Dari 10 film yang direkomendasikan, seluruhnya memiliki genre yang sama persis dengan film Toy Story. Oleh karena itu, sistem menghasilkan nilai evaluasi:

![Precision](https://raw.githubusercontent.com/LapplandSa/Proyek-Sistem-Rekomendasi/main/images/result3.png)

Precision@10: 1.0

Nilai ini menunjukkan bahwa 100% dari rekomendasi yang diberikan sistem benar-benar relevan dengan preferensi pengguna berdasarkan kesamaan konten. Hasil ini mengindikasikan bahwa metode Content-Based Filtering yang diterapkan mampu secara akurat mengenali dan merekomendasikan film-film dengan genre yang identik, sesuai dengan preferensi awal pengguna.

### Evaluation untuk Collaborative Filtering

![RMSE](https://raw.githubusercontent.com/LapplandSa/Proyek-Sistem-Rekomendasi/main/images/RMSE.png)

Evaluasi model Collaborative Filtering dilakukan dengan menggunakan metrik Root Mean Squared Error (RMSE), yang mengukur seberapa jauh prediksi rating yang dihasilkan model menyimpang dari rating asli yang diberikan oleh pengguna.

![RMSE](https://raw.githubusercontent.com/LapplandSa/Proyek-Sistem-Rekomendasi/main/images/result4.png)

Pada pengujian dengan data testing, model berhasil mencapai nilai RMSE sebesar 0.9623. Nilai ini menunjukkan bahwa rata-rata kesalahan prediksi model terhadap rating asli adalah sekitar 0.96 pada skala rating 0–5. Dengan kata lain, model dapat memprediksi preferensi pengguna terhadap film dengan tingkat akurasi yang cukup baik.

RMSE ini memberikan gambaran seberapa tepat model Collaborative Filtering dalam merekomendasikan film berdasarkan interaksi pengguna secara historis, dan menjadi indikator utama untuk menilai kualitas sistem rekomendasi berbasis data pengguna dan item.

### Keterkaitan dengan Business Understanding

Evaluasi performa model dalam proyek ini memberikan kontribusi signifikan terhadap pemahaman bisnis, khususnya dalam menjawab kebutuhan utama pengguna platform streaming: mengurangi kebingungan dalam memilih film dan meningkatkan kepuasan pengalaman menonton. Dua pendekatan utama yang digunakan, yaitu Content-Based Filtering dan Collaborative Filtering, diuji performanya menggunakan metrik evaluasi yang sesuai dengan tujuan bisnis: personalisasi dan akurasi.

Model Collaborative Filtering (Neural Network) mencapai RMSE sebesar 0.9623, yang menunjukkan bahwa model mampu memprediksi rating pengguna terhadap film dengan kesalahan yang relatif kecil. Artinya, rekomendasi yang diberikan mendekati preferensi aktual pengguna, sehingga berpotensi meningkatkan engagement dan loyalitas pengguna terhadap platform.

### Keterkaitan dengan Problem Statements

**Mengatasi banyaknya pilihan film (information overload):**

Dengan menghasilkan 10 rekomendasi film yang paling sesuai berdasarkan estimasi rating tertinggi, sistem membantu pengguna dalam menyaring ribuan film yang tersedia, sehingga secara langsung mengatasi Problem Statement 1 mengenai overload informasi.

**Memberikan rekomendasi yang relevan secara personal:**

Model rekomendasi yang dikembangkan berhasil memberikan daftar film yang relevan secara personal berdasarkan preferensi pengguna. Sebagai contoh, untuk User ID 1, sistem merekomendasikan sejumlah film dengan prediksi rating tinggi, seperti The Usual Suspects, Star Wars: Episode IV - A New Hope, Forrest Gump, Princess Bride, The, dan Raiders of the Lost Ark. Film-film tersebut umumnya memiliki genre dan karakteristik yang sejalan dengan minat pengguna, sehingga menunjukkan kemampuan model dalam menangkap selera dan memberikan rekomendasi yang tepat. Hasil ini secara langsung menjawab kebutuhan dalam Problem Statement 2, yang menekankan pentingnya relevansi dan personalisasi dalam sistem rekomendasi untuk meningkatkan kepuasan pengguna.

### Evaluasi Terhadap Goals

**Membangun sistem rekomendasi personalisasi:**

Tercapai melalui dua pendekatan utama:

- Content-Based Filtering menggunakan genre dan tahun rilis film yang diproses dengan TF-IDF dan cosine similarity.

- Collaborative Filtering dengan embedding pengguna dan film menggunakan neural network untuk mempelajari preferensi secara implisit.

Kedua sistem menghasilkan rekomendasi film yang sesuai dengan preferensi pengguna, baik berdasarkan konten maupun perilaku pengguna lain.

**Meningkatkan relevansi melalui data historis:**

Collaborative Filtering terbukti mampu memanfaatkan data rating historis secara efektif. RMSE sebesar 0.9623 mengindikasikan bahwa prediksi rating cukup akurat. Hal ini menunjukkan bahwa sistem dapat diandalkan dalam memberikan prediksi terhadap film yang belum pernah ditonton oleh pengguna, memperkuat pencapaian Goals.

### Dampak dari Solution Statements

**Content-Based Filtering:**

Pendekatan Content-Based Filtering yang digunakan berhasil mengatasi masalah cold-start, khususnya untuk pengguna baru yang belum memiliki data interaksi sebelumnya. Sistem memanfaatkan informasi metadata film, yaitu genre dan tahun rilis, yang diolah menggunakan teknik TF-IDF dan diukur kemiripannya dengan cosine similarity. Dengan cara ini, sistem dapat merekomendasikan film-film yang memiliki kemiripan konten dengan film yang sudah disukai pengguna sebelumnya.

Sebagai contoh, untuk film Toy Story, sistem memberikan rekomendasi film-film lain yang memiliki genre serupa, yaitu Adventure, Animation, Children, Comedy, dan Fantasy, meskipun tahun rilisnya bervariasi. Beberapa film yang direkomendasikan antara lain Wild, The (2006), Asterix and the Vikings (2006), Monsters, Inc. (2001), Shrek the Third (2007), dan Toy Story 2 (1999). Rekomendasi ini menunjukkan bahwa model mampu mengenali kesamaan genre secara efektif untuk menghasilkan daftar film yang relevan dan sesuai dengan preferensi konten pengguna.

**Collaborative Filtering:**

Pendekatan Collaborative Filtering yang diterapkan menggunakan embedding pengguna dan film yang dipelajari melalui neural network. Dengan cara ini, sistem tidak hanya bergantung pada metadata film seperti genre atau tahun, tetapi juga pada pola interaksi riil dari seluruh pengguna, seperti rating yang diberikan terhadap film-film tertentu. Embedding ini merepresentasikan preferensi pengguna dan karakteristik film dalam ruang fitur berdimensi rendah, sehingga memungkinkan model mengenali hubungan kompleks yang tidak terlihat secara eksplisit dari metadata.

Keunggulan metode ini adalah kemampuannya untuk menangkap preferensi individual pengguna dengan lebih akurat, termasuk minat yang unik dan tidak mudah dijelaskan hanya dengan genre atau atribut lain. Misalnya, dua pengguna yang menyukai film dengan genre berbeda tapi memiliki kesamaan dalam pola rating film tertentu dapat diberikan rekomendasi yang relevan berdasarkan kesamaan embedding mereka.

Dengan demikian, Collaborative Filtering mampu memberikan rekomendasi yang lebih personal dan bermakna, meningkatkan kepuasan pengguna karena sistem belajar dari perilaku kolektif dan preferensi tersembunyi yang tidak dapat diwakili oleh metode berbasis konten saja.
