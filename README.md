# Proyek Akhir : Membuat Model Sistem Rekomendasi

## Project Overview
Perusahaan *e-commerce* seperti Amazon biasanya menggunakan sistem rekomendasi yang berbeda untuk memberikan saran kepada pelanggan. Amazon saat ini menggunakan *collaborative filtering items*, yang menskalakan kumpulan dataset dan menghasilkan sistem rekomendasi berkualitas tinggi secara *real time*. Jenis pemfilteran ini mencocokkan setiap item yang dibeli dan diberi peringkat oleh pengguna dengan item serupa, lalu menggabungkan item serupa tersebut ke dalam daftar rekomendasi untuk pengguna. Dalam proyek ini akan dibuat model rekomendasi untuk produk elektronik Amazon. Sistem ini adalah sistem penyaringan informasi yang berusaha untuk memberikan rekomendasi produk teratas yang diminati oleh pengguna.

## Business Understanding
Pelanggan yang mengunjungi website tentu ingin pengalaman yang terbaik. Hal tersebut memicu sistem *e-commerce* untuk terus beradaptasi dan terus menyesuaikan keinginan pelanggan. Ketika pelanggan melakukan pencarian tanpa adanya rekomendasi lainnya, pelanggan akan cenderung langsung meninggalkan *e-commerce* dan ini tentu akan merugikan perusahaan.

### Problem Statements
Pernyataan masalah yang terdapat dalam proyek ini, yakni:
- Pelanggan yang meninggalkan website setelah barang yang diinginkan terpenuhi
- Tingkat pengunjung yang rendah karena tidak adanya sistem rekomendasi
- Kurang efektifnya tingkat rekomendasi secara clustering

### Goals / Project Summary
Menjelaskan tujuan proyek yang akan menjawab pernyataan masalah:
- Dapat merekomendasikan barang lain sehingga pelanggan tidak cepat cepat untuk pergi dari website
- Meningkatkan tingkat pengunjung website dengan menampilkan rekomendasi sehingga pelanggan tetap betah di dalam website
- Membuat model serta mengevaluasi model dengan Metriks MSE dan LOSS sehingga lebih cepat

## Data Understanding
Dataset pada proyek ini diperoleh dari Kaggle: https://www.kaggle.com/datasets/saurav9786/amazon-product-reviews

Berikut fitur-fitur yang terdapat pada dataset dan deskripsinya:
- userId = ID user yang telah melakukan pembelian pada produk di website
- productId = ID produk yang telah dibeli oleh user
- rating = Rating dari produk yang dinilai oleh user pada produk
- timestamp = Tanggal terjadinya transaksi

### Exploratory Data Analysis
Berikut beberapa teknik visualisasi data beserta insight yang didapatkan dari dataset ini:

- Melihat data berdasarkan waktu dan ratingnya

![image4](https://user-images.githubusercontent.com/99348807/204231808-2f99cf39-c3a5-41a7-8aca-1f2ce980c9b2.jpg)

- Melihat grafik trends berdasarkan waktu dan total pemberian rating

![image5](https://user-images.githubusercontent.com/99348807/204231811-8be61473-0243-4570-bfd3-2f58419ea4fd.jpg)

- Melihat banyaknya persebaran rating yang diberikan oleh pengguna
-
![image6](https://user-images.githubusercontent.com/99348807/204231812-00cebaf3-c54e-4279-b754-38820ddaf898.jpg)

- Melihat produk teratas berdasarkan jumlah rating

![image7](https://user-images.githubusercontent.com/99348807/204231813-23da8b20-b92a-4ff1-b411-8802c7eb99cd.jpg)

## Data Preparation / Data Preprocessing
Pengolahan data dilakukan dalam beberapa tahap mulai dari mengubah string menjadi list hingga menyusun algoritma. Berikut detail Data Preparation yang dilakukan:
- Tahap 1: Memasukkan data, sebelumnya tabel yang ada tidak ada nama kolomnya. Tampilannya seperti di bawah ini:

![image1](https://user-images.githubusercontent.com/99348807/204231793-5465cf37-63c2-4860-ac40-2e0f5bdcb349.jpg)

- Tahap 2: Dengan melihat dokumentasi sumber data, dilakukan rename kolom sehingga akan tampil seperti di bawah ini:

![image2](https://user-images.githubusercontent.com/99348807/204231802-59ab79f6-911e-4508-9545-d2772eaba912.jpg)

- Tahap 3: Setelah data tampil, tahap selanjutnya ialah mengecek ketersediaan isi pada kolom, karena ketika ada missing kolom akan menyebabkan sistem rekomendasi kurang optimal

![image3](https://user-images.githubusercontent.com/99348807/204231806-f1829b43-7355-4fd4-9c0e-087b13275c63.jpg)

Pengolahan data sampai di tahap ini, selanjutnya data yang sudah bersih akan diolah pada modelling.

## Modeling and Result
### Modeling
Modeling pada proyek ini dilakukan dengan TensorFlow Recommenders (TFRS). TensorFlow Recommenders (TFRS) adalah library untuk membuat model sistem pemberi rekomendasi. Model ini dibangun menggunakan Keras dan bertujuan untuk memiliki kurva belajar yang lembut sambil tetap memberi fleksibilitas untuk membuat model yang kompleks. Beberapa tahapan yang dilakukan, yakni:
- Tahap 1: Mendefinisikan ranking model yang merupakan library dari tensorflow untuk tiap tiap kolom Rating, UserID, dan ProdukID.

- Tahap 2: Setting untuk setiap model yang dilatih, supaya saat model pelatihan tidak terdapat duplikat yang menyebabkan memori berlebih dengan code di bawah ini:
```
userIds    = recent_prod.userId.unique()
productIds = recent_prod.productId.unique()
total_ratings= len(recent_prod.index)
```
- Tahap 3: Melakukan *training* atau pelatihan model berdasarkan metriks RMSE, Loss dan memberikan hasil seperti di bawah ini:

![image8](https://user-images.githubusercontent.com/99348807/204238920-398a96f5-d7b3-4a02-acd0-8fc9fc251640.jpg)

### Result
- Tahap 4: Uji coba prediksi dengan memanggil function model dengan parameter user id. Berikut hasil yang ditampilkan:
Keterangan : untuk produk ID yang tampil
```
B002FFG6JC
B004ABO7QI
B006YW3DI4
B0012YJQWQ
B006ZBWV0K
```

## Evaluation
Pada proyek ini digunakan metriks RMSE untuk pelatihan model. RMSE merupakan singkatan dari Root Means Squared Error. Berikut merupakan rumus dari RMSE: 

![images9](https://user-images.githubusercontent.com/99348807/204239677-f7d933c3-6815-4a03-b512-62ed2a4660dc.png)

Dalam penggunaan machine learning sistem rekomendasi ini, RMSE berperan untuk mencari bobot besar berdasarkan loss yang besar. RMSE digunakan karena tidak menginginkan outlier pada model. Hasil yang didapat dari RMSE cukup memuaskan (terdapat pada tahap 4). Dengan begitu, goals diawal untuk membuat rekomendasi yang sebelumnya menggunakan clustering berhasil dibuat dengan performa yang baik. Sehingga, ketika diterapkan di dalam model bisnis *e-commerce* pengguna tidak akan langsung meninggalkan *e-commerce* dengan cepat karena akan muncul item yang direkomendasikan. Tetapi, pengguna dapat melihat lihat rekomendasi dari produk yang bersangkutan dan hal itu dapat meningkatkan tingkat keramaian website.
