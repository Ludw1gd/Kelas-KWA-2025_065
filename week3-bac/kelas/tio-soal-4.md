# Write-up Juice-Shop: Five Star Feedback

## Ringkasan Tantangan

**Judul:** Five-Star Feedback 

**Kategori:** Broken Access Control (Kontrol Akses yang Rusak)  
**Tingkat Kesulitan:** ⭐⭐ (2/6)

Tantangan "Five Star Feedback" ini menuntut kita untuk memanipulasi sistem ulasan pada aplikasi web dengan cara menghapus semua ulasan yang memiliki rating bintang lima.

---

## Alat yang Digunakan

- **Peramban Web (Web Browser)**: Untuk berinteraksi dengan dasbor administrasi aplikasi.
- **Akses ke Panel Admin**: Memanfaatkan akses administratif yang telah diperoleh sebelumnya untuk menavigasi dan memodifikasi data aplikasi.

---

## Metodologi dan Solusi

Untuk menyelesaikan tantangan ini, kita perlu memanfaatkan akses admin yang sudah kita miliki untuk mengelola data umpan balik pengguna.

### 1. Mengakses Panel Admin dan Mengelola Umpan Balik

- **Memanfaatkan Hak Akses Administratif**: Dari tantangan sebelumnya, kita telah mendapatkan akses sebagai administrator. Akses ini memungkinkan kita untuk menjelajahi fungsionalitas yang tidak tersedia bagi pengguna biasa, termasuk pengelolaan umpan balik pengguna.
- **Menemukan Bagian Pengelolaan Umpan Balik**: Di dalam panel admin (`/#/administration`), navigasikan ke bagian tempat ulasan dan umpan balik dari pengguna dikelola ("User Feedback").

### 2. Menghapus Ulasan Bintang Lima

- **Mengidentifikasi dan Menghapus Ulasan**: Di halaman pengelolaan umpan balik, semua ulasan pengguna akan ditampilkan beserta peringkat bintangnya. Identifikasi semua ulasan dengan peringkat bintang lima, lalu hapus satu per satu menggunakan tombol hapus yang tersedia di samping setiap ulasan.


*Gambar 1: Tampilan panel admin yang menunjukkan daftar umpan balik pengguna beserta tombol hapus.*
<img width="998" height="957" alt="image" src="https://github.com/user-attachments/assets/80056560-c36c-4742-bfea-aa832b0667fa" />

---

## Penjelasan Solusi

Tantangan ini berhasil diselesaikan dengan mengeksploitasi kelemahan pada kontrol akses. Seharusnya, tindakan menghapus umpan balik dibatasi hanya untuk personel yang berwenang. Kerentanan ini menunjukkan bahwa bahkan pengguna yang memiliki hak akses admin dapat menyalahgunakan wewenang jika tidak ada mekanisme pengawasan atau batasan yang tepat.

---

## Rekomendasi Perbaikan (Remediasi)

Untuk melindungi dari kerentanan serupa di aplikasi dunia nyata, pertimbangkan langkah-langkah berikut:

- **Kontrol Akses Berbasis Peran (RBAC)**: Pastikan hanya personel yang berwenang yang memiliki kemampuan untuk mengubah atau menghapus konten buatan pengguna. Terapkan kebijakan RBAC yang ketat yang mendefinisikan siapa dapat melakukan tindakan apa di dalam panel admin.
- **Jejak Audit (Audit Trails)**: Simpan jejak audit yang mencatat semua tindakan administratif, terutama yang memengaruhi data atau umpan balik pengguna. Ini membantu dalam akuntabilitas dan melacak bagaimana tindakan tertentu diizinkan atau dieksekusi.
- **Justifikasi Penghapusan Ulasan**: Terapkan mekanisme yang mewajibkan administrator untuk memberikan alasan atau justifikasi saat menghapus konten dalam jumlah besar, terutama konten positif yang bisa disalahgunakan.
