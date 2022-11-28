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


## Data Preparation / Data Preprocessing
Dalam mengelola data dilakukan beberapa pembersihan data yaitu mengubah string menjadi list hingga menyusun algoritma KNN untuk Clustering, detailnya:
- Tahap 1: Memasukkan data, sebelumnya tabel yang ada tidak ada nama kolomnya tampil seperti ini :
- Tahap 2: Dengan melihat dokumentasi sumber data, penulis melakukan rename kolom sehingga tanpak seperti ini :
- Tahap 3: Seperti yang diajarkan dalam modul, pada tahap ini penulis berusaha untuk mempelajari distribusi data dan isinya dengan melakukan sintaks berikut ini:
- Tahap 4: Setelah data muncul, tahap selanjutnya adalah mengecek ketersediaan isi pada kolom, karena ketika ada missing kolom ini akan menyebabkan sistem rekomendasi kurang optimal
- Tahap 5: Mempelajari data dari parameter waktu dan rating, dengan begitu bisa dilihat bahwa untuk pemberian rating terbanyak itu pada tahun 2014 (gambar dibawah)

Pengolahan data sampai di tahap ini, selanjutnya data yang sudah bersih ini akan diolah pada segment modelling


## Modeling and Result
Pada tahap modelling ini digunakan algoritma KNN dengan tambahan tokenizer untuk mengidentifikasi kata kata yang sekolompok. Tidak hanya itu untuk memerbaiki kinerja dari program, ditambahkan *stop-word* supaya kata-kata yang diambil dalam bahasa inggris ini bukan kata penghubung dasar dan kata kerja dasar, melainkan benar-benar objek. Beberapa tahapan saat modelling, yakni:

- Tahap 1: Mendefinisikan ranking model merupakan library dari tensorflow untuk tiap tiap kolom Rating, UserID, dan ProdukID, dengan bantuan tensorflow

- Tahap 2: Setting untuk setiap model yang dilatih, supaya saat model pelatihan tidak terdapat duplikat yang menyebabkan memori berlebih dengan code ini:
```
userIds    = recent_prod.userId.unique()
productIds = recent_prod.productId.unique()
total_ratings= len(recent_prod.index)
```
- Tahap 3: Lakukan model training berdasarkan metriks RMSE, Loss yang sudah dituliskan pada code menjadi seperti dibawah ini. Untuk penjelasan metriks akan ada di tahap evaluation

- Tahap 4: Uji coba prediksi dengan memanggil function model dengan parameter user id, sehingga menjadi:
Keterangan : untuk produk ID yang tampil
```
B002FFG6JC
B004ABO7QI
B006YW3DI4
B0012YJQWQ
B006ZBWV0K
```

## Evaluation

