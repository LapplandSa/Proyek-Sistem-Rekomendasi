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

## Modeling

Pada tahap ini, dibangun dua model sistem rekomendasi menggunakan pendekatan yang berbeda: Content-Based Filtering dan Collaborative Filtering berbasis model Neural Network. Pendekatan ini dipilih untuk saling melengkapi dalam memberikan rekomendasi yang lebih relevan dan akurat kepada pengguna.

### Content-Based Filtering

Pendekatan ini merekomendasikan film berdasarkan kemiripan konten dengan film yang sebelumnya disukai oleh pengguna. Informasi konten yang digunakan dalam model ini adalah genre dan tahun rilis film.

**Langkah-langkah:**

- Genre diformat menggunakan TF-IDF Vectorizer untuk menghasilkan representasi fitur dari setiap film.

- Cosine similarity dihitung antar film berdasarkan vektor genre.

- Tahun film kemudian turut dipertimbangkan sebagai faktor tambahan untuk meningkatkan relevansi.

- Untuk pengguna tertentu, sistem mengidentifikasi film yang telah mereka beri rating tinggi, lalu mencari film lain yang memiliki kemiripan tertinggi (berdasarkan genre dan tahun) dengan film tersebut.

- Top-N film dengan skor kemiripan tertinggi disarankan sebagai rekomendasi.

**Output:**

![Result](https://raw.githubusercontent.com/LapplandSa/Proyek-Sistem-Rekomendasi/main/images/result1.png)

Output di atas merupakan hasil dari sistem Content-Based Filtering yang merekomendasikan film berdasarkan kemiripan kontennya, khususnya genre dan tahun rilis. Film yang direkomendasikan seperti Balto, Jumanji, dan Indian in the Cupboard, The menunjukkan kecenderungan kesamaan pada genre Adventure, Children, dan Fantasy. Selain itu, semua film yang muncul dalam rekomendasi berasal dari tahun yang sama, yaitu 1995, yang menunjukkan bahwa sistem juga mempertimbangkan kemiripan waktu rilis sebagai faktor penentu relevansi. Ini penting karena preferensi terhadap film sering kali berkaitan dengan era atau periode tertentu. Dengan demikian, rekomendasi yang diberikan bersifat personal dan kontekstual, menyesuaikan dengan gaya dan era film yang kemungkinan besar disukai oleh pengguna.

**Kelebihan:**

- Cocok untuk menangani cold start problem, terutama ketika data rating pengguna masih sedikit.

- Dapat memberikan alasan rekomendasi yang jelas, misalnya karena film memiliki genre yang sama.

**Kekurangan:**

- Bergantung penuh pada metadata; jika informasi konten terbatas atau tidak akurat, kualitas rekomendasi menurun.

- Tidak memperhitungkan pola kesukaan kolektif dari pengguna lain.

### Collaborative Filtering Berbasis Model (Neural Network)

Model ini mempelajari pola interaksi antara pengguna dan film menggunakan representasi embedding dan memprediksi rating yang mungkin diberikan pengguna ke film yang belum ditonton.

**Langkah-langkah:**

- Dibangun model RecommenderNet dengan TensorFlow, terdiri dari dua embedding layer (untuk user dan item), dilanjutkan dengan dot product.

- Input berupa pasangan userId dan movieId.

- Target adalah rating aktual pengguna terhadap film.

- Setelah pelatihan, sistem memprediksi rating dari semua film yang belum ditonton oleh pengguna, kemudian mengurutkan berdasarkan nilai prediksi tertinggi.

**Output:**

![Result](https://raw.githubusercontent.com/LapplandSa/Proyek-Sistem-Rekomendasi/main/images/result2.png)

Output di atas merupakan hasil dari sistem Collaborative Filtering berbasis model (Neural Network), yang memberikan rekomendasi film untuk User ID 1. Rekomendasi ini dihasilkan berdasarkan pola rating yang serupa dari pengguna lain yang memiliki preferensi mirip. Sistem memperkirakan rating yang mungkin diberikan oleh pengguna terhadap film-film yang belum ditonton, kemudian mengurutkannya berdasarkan nilai predicted rating tertinggi. Misalnya, film "The Usual Suspects", "The Shawshank Redemption", dan "The Dark Knight" memiliki nilai prediksi di atas 4.5, yang menunjukkan bahwa sistem memperkirakan pengguna ini sangat mungkin menyukai film-film tersebut. Hasil ini menunjukkan bahwa model mampu menangkap preferensi pengguna dan memberikan saran yang relevan berdasarkan perilaku kolektif pengguna lain dalam dataset.

**Kelebihan:**

- Mampu menangkap pola kompleks antara pengguna dan item.

- Rekomendasi bersifat personalized berdasarkan preferensi pengguna.

**Kekurangan:**

- Membutuhkan cukup banyak data rating agar dapat belajar representasi dengan baik.

- Tidak dapat bekerja optimal pada pengguna baru (cold start problem).

## Evaluation

### Evaluation untuk Collaborative Filtering

Untuk mengevaluasi performa sistem rekomendasi berbasis Collaborative Filtering dengan Neural Network, metrik yang digunakan adalah Root Mean Squared Error (RMSE). RMSE mengukur seberapa jauh nilai rating yang diprediksi oleh model dibandingkan dengan rating sebenarnya yang diberikan oleh pengguna. Nilai RMSE yang lebih kecil menandakan bahwa prediksi model lebih akurat.

![RMSE](https://raw.githubusercontent.com/LapplandSa/Proyek-Sistem-Rekomendasi/main/images/RMSE.png)

Dalam konteks proyek ini, RMSE digunakan untuk mengetahui seberapa akurat model dalam memprediksi rating yang akan diberikan oleh pengguna terhadap film tertentu. Hasil evaluasi menunjukkan bahwa model menghasilkan nilai RMSE sebesar 0.8785, yang berarti secara rata-rata prediksi model hanya meleset sekitar 0.88 poin dari rating aktual. Ini mengindikasikan bahwa model telah belajar dengan cukup baik untuk merepresentasikan preferensi pengguna terhadap film.

Untuk pendekatan Content-Based Filtering, metrik evaluasi eksplisit seperti RMSE tidak digunakan karena sistem ini tidak memprediksi rating secara langsung. Sebagai gantinya, evaluasi dilakukan secara kualitatif dengan meninjau hasil rekomendasi apakah relevan atau tidak berdasarkan kemiripan konten (genre dan tahun) dari film yang disukai pengguna. Misalnya, untuk User ID 1, sistem berhasil merekomendasikan film yang memiliki kemiripan genre dan tahun dengan film yang telah mereka beri rating tinggi.

### Evaluation untuk Content-Based Filtering

Berbeda dengan Collaborative Filtering yang memprediksi rating dan dievaluasi menggunakan metrik regresi seperti RMSE, pendekatan Content-Based Filtering bertujuan merekomendasikan item berdasarkan kemiripan kontennya (dalam hal ini, genre dan tahun rilis film). Oleh karena itu, metrik evaluasi kuantitatif seperti RMSE tidak relevan.

Sebagai gantinya, performa Content-Based Filtering umumnya dievaluasi melalui:

- Validasi manual: dengan melihat apakah film yang direkomendasikan memang mirip atau relevan dengan film yang disukai pengguna.

- Studi user feedback: meminta pengguna untuk menilai apakah rekomendasi yang diberikan sesuai dengan preferensi mereka.

- Precision@k atau Recall@k (jika tersedia data historis yang cukup): untuk mengukur berapa banyak film yang benar-benar disukai dari daftar rekomendasi.

Namun, dalam proyek ini, karena tidak dilakukan evaluasi berbasis feedback pengguna secara eksplisit, maka hasil evaluasi Content-Based Filtering ditunjukkan melalui analisis kualitatif: yaitu dengan melihat kesesuaian genre dan tahun dari film-film yang direkomendasikan dengan film yang sebelumnya disukai oleh pengguna. Pendekatan ini juga bermanfaat pada situasi cold-start, di mana data interaksi pengguna sangat terbatas.

Sebagai contoh, ketika pengguna menyukai film Toy Story, sistem merekomendasikan film lain seperti Jumanji, Balto, dan Wallace & Gromit: A Close Shave. Film-film ini memiliki genre serupa, yaitu Adventure, Animation, dan Children, serta dirilis pada tahun yang sama (1995). Hal ini menunjukkan bahwa sistem dapat mengenali kemiripan berdasarkan konten (genre + tahun), dan mampu memberikan rekomendasi yang konsisten dengan preferensi pengguna.
