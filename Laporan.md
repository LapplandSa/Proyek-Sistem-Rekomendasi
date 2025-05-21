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

1. Tingginya jumlah pilihan film menyebabkan pengguna mengalami kesulitan dalam menemukan tontonan yang sesuai preferensi pribadi.

   Dengan ribuan judul film tersedia di platform digital, pengguna seringkali mengalami information overload sehingga memerlukan bantuan sistem yang mampu menyaring dan merekomendasikan film secara efisien.

2. Sistem rekomendasi yang bersifat generik tidak mampu memberikan saran yang relevan secara personal.

   Rekomendasi yang tidak mempertimbangkan pola perilaku unik dan preferensi spesifik pengguna berpotensi menghasilkan saran film yang tidak menarik, sehingga menurunkan kepuasan dan engagement pengguna.

3. Kurangnya integrasi antara data konten film dan perilaku pengguna dalam sistem rekomendasi menurunkan akurasi hasil rekomendasi.
  
   Banyak sistem hanya mengandalkan pendekatan tunggal, seperti content-based filtering atau collaborative filtering, padahal kombinasi keduanya secara hibrida berpotensi menghasilkan rekomendasi yang lebih tepat dan kontekstual.

### Goals

1. Mengembangkan sistem rekomendasi film yang mampu mempersonalisasi saran tontonan berdasarkan preferensi pengguna.
  
   Sistem ini dirancang untuk membantu pengguna menyaring ribuan film secara efisien dan menyarankan film yang paling relevan dengan selera mereka, sehingga mengurangi kebingungan dalam memilih.

2. Meningkatkan relevansi rekomendasi melalui pemanfaatan data historis perilaku pengguna.

   Sistem akan belajar dari pola penilaian dan interaksi pengguna untuk menghasilkan saran film yang sesuai dengan kebiasaan menonton masing-masing individu.

3. Membangun model rekomendasi hibrida dengan menggabungkan pendekatan content-based dan collaborative filtering.

   Dengan memanfaatkan informasi konten film (seperti genre) serta data interaksi pengguna (seperti rating), sistem ini diharapkan dapat memberikan prediksi yang lebih akurat dan kontekstual dibandingkan dengan pendekatan tunggal.

### Solution statements

1. Content-Based Filtering

Pendekatan ini memanfaatkan metadata film, seperti genre, untuk menghitung tingkat kemiripan antar film menggunakan teknik ekstraksi fitur seperti TF-IDF (Term Frequency-Inverse Document Frequency) dan pengukuran kesamaan menggunakan cosine similarity. Sistem kemudian merekomendasikan film yang memiliki kemiripan konten dengan film-film yang sebelumnya disukai oleh pengguna. Pendekatan ini sangat efektif untuk menangani masalah cold-start pada pengguna baru atau ketika data rating masih terbatas.

2. Collaborative Filtering

Metode ini membangun representasi vektor (embedding) untuk setiap pengguna dan film berdasarkan pola interaksi dan rating yang diberikan. Dengan menggunakan model neural network, seperti RecommenderNet yang dikembangkan menggunakan TensorFlow, sistem mempelajari hubungan kompleks antara pengguna dan film melalui embedding layer dan operasi dot product untuk memprediksi rating atau preferensi pengguna terhadap film yang belum pernah ditonton. Pendekatan ini memungkinkan rekomendasi yang lebih personal dan akurat dengan memanfaatkan data interaksi pengguna secara kolektif.

## Data Understanding
Paragraf awal bagian ini menjelaskan informasi mengenai jumlah data, kondisi data, dan informasi mengenai data yang digunakan. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Selanjutnya, uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
