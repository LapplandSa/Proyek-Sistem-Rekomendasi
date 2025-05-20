# Laporan Proyek Machine Learning - Moch. Yusuf Haidar Ali Ramdhani
# Proyek Sistem Rekomendasi

## Project Overview

Dalam era digital saat ini, jumlah film yang tersedia secara online semakin meningkat, baik melalui platform streaming maupun katalog digital lainnya. Hal ini menyebabkan pengguna kesulitan dalam memilih film yang sesuai dengan preferensi mereka. Oleh karena itu, sistem rekomendasi film menjadi sangat penting untuk membantu pengguna menemukan film yang relevan dan menarik bagi mereka.

Sistem rekomendasi telah menjadi komponen kunci dalam banyak aplikasi modern, terutama di industri hiburan seperti Netflix, Amazon Prime Video, dan Disney+. Menurut Ricci et al. [1], sistem rekomendasi bertujuan untuk memberikan saran item yang paling relevan kepada pengguna berdasarkan preferensi atau perilaku sebelumnya. Pendekatan umum dalam sistem rekomendasi adalah content-based filtering dan collaborative filtering.

Dalam proyek ini, akan dikembangkan sistem rekomendasi film menggunakan kedua pendekatan tersebut:

Content-Based Filtering akan memanfaatkan metadata film, seperti genre, untuk merekomendasikan film yang mirip dengan yang telah disukai pengguna.

Collaborative Filtering, terutama dengan pendekatan model embedding menggunakan TensorFlow, akan memanfaatkan pola rating dari pengguna lain untuk memberikan rekomendasi yang lebih personal.

Masalah ini penting untuk diselesaikan karena relevansi rekomendasi sangat berpengaruh terhadap kepuasan pengguna. Tanpa sistem yang baik, pengguna bisa kehilangan minat atau menghabiskan waktu lebih lama untuk mencari tontonan, yang pada akhirnya berdampak pada engagement dan retensi pengguna dalam aplikasi.

Data yang digunakan dalam proyek ini berasal dari MovieLens, salah satu dataset benchmark paling umum dalam pengembangan sistem rekomendasi. MovieLens dikembangkan oleh GroupLens Research dan telah digunakan dalam berbagai penelitian akademik [2].

Dengan menggabungkan dua pendekatan utama dalam sistem rekomendasi, proyek ini bertujuan untuk menghasilkan sistem yang lebih akurat dan mampu memberikan saran film yang lebih relevan dan dipersonalisasi.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Jelaskan mengapa dan bagaimana masalah tersebut harus diselesaikan
- Menyertakan hasil riset terkait atau referensi. Referensi yang diberikan harus berasal dari sumber yang kredibel dan author yang jelas.
- Format Referensi dapat mengacu pada penulisan sitasi [IEEE](https://journals.ieeeauthorcenter.ieee.org/wp-content/uploads/sites/7/IEEE_Reference_Guide.pdf), [APA](https://www.mendeley.com/guides/apa-citation-guide/) atau secara umum seperti [di sini](https://penerbitdeepublish.com/menulis-buku-membuat-sitasi-dengan-mudah/)
- Sumber yang bisa digunakan [Scholar](https://scholar.google.com/)

## Business Understanding

Pada bagian ini, Anda perlu menjelaskan proses klarifikasi masalah.

Bagian laporan ini mencakup:

### Problem Statements

Pengguna kesulitan menemukan film yang sesuai dengan preferensi mereka.
Dengan jumlah film yang sangat banyak dalam katalog, pengguna seringkali bingung menentukan pilihan tontonan yang sesuai selera.

Rekomendasi film yang tidak personal mengurangi minat pengguna.
Sistem rekomendasi konvensional yang tidak memperhatikan preferensi individual cenderung menghasilkan saran yang kurang relevan.

Kurangnya integrasi antara informasi konten film dan pola perilaku pengguna.
Banyak sistem hanya menggunakan satu pendekatan saja (misalnya genre), padahal gabungan informasi konten dan perilaku bisa memberikan hasil yang lebih akurat.

### Goals

Membuat sistem yang dapat memberikan rekomendasi film berdasarkan preferensi pengguna.
Sistem ini diharapkan mampu menyarankan film dengan genre atau karakteristik yang mirip dengan film yang pernah disukai pengguna.

Meningkatkan personalisasi rekomendasi menggunakan data perilaku pengguna.
Dengan memanfaatkan data rating pengguna lain, sistem dapat menyarankan film yang cenderung disukai oleh pengguna dengan perilaku serupa.

Menguji efektivitas gabungan pendekatan content-based dan collaborative filtering.
Sistem akan dibangun dan dievaluasi dengan dua metode untuk melihat mana yang paling efektif, atau apakah kombinasi keduanya menghasilkan hasil terbaik.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Menambahkan bagian “Solution Approach” yang menguraikan cara untuk meraih goals. Bagian ini dibuat dengan ketentuan sebagai berikut: 

    ### Solution statements
    - Mengajukan 2 atau lebih solution approach (algoritma atau pendekatan sistem rekomendasi).

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
