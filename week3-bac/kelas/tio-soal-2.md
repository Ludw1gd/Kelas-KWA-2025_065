# Write-up Juice-Shop: Bagian Admin

## Ringkasan Tantangan

**Judul:** Bagian Admin (Admin Section)  
**Kategori:** Broken Access Control (Kontrol Akses yang Rusak)  
**Tingkat Kesulitan:** ⭐⭐ (2/6)

Tantangan "Bagian Admin" ini adalah tentang mengakses area administratif terlarang dari sebuah aplikasi web yang seharusnya tidak dapat dijangkau oleh pengguna biasa.

---

## Alat yang Digunakan

- **Peramban Web (Web Browser)**: Untuk mengakses aplikasi dan menggunakan *developer tools*.
- **Alat Pengembang (Developer Tools)**: Khususnya untuk memeriksa kode sumber (file JavaScript) untuk menemukan definisi rute aplikasi.

---

## Metodologi dan Solusi

Langkah penyelesaian tantangan ini melibatkan penemuan *endpoint* atau path tersembunyi dan kemudian mendapatkan hak akses yang tepat untuk membukanya.

### 1. Menemukan Rute Tersembunyi dan Percobaan Akses

Pertama, kita perlu mengetahui alamat dari halaman admin. Dengan asumsi kita tidak mengetahuinya, kita bisa mencarinya di dalam file sumber aplikasi. Namun, jika kita sudah menduga path-nya, kita bisa langsung mencobanya.

- **Akses Langsung ke Path**: Mencoba mengakses path `/administration` secara langsung dengan mengetikkannya di bilah alamat peramban.
- Upaya awal ini akan gagal dan menampilkan pesan kesalahan karena kita belum login sebagai pengguna dengan hak akses yang cukup.


*Gambar 1: Akses ditolak saat mencoba masuk ke `/administration` tanpa izin.*

<img width="2524" height="1469" alt="image" src="https://github.com/user-attachments/assets/712c5d65-eda4-4ec7-97b0-f09a25921825" />

---

### 2. Mendapatkan Akses Administratif

Untuk melewati pembatasan akses, kita harus masuk sebagai administrator.

- **Peningkatan Peran (Role Elevation)**: Login menggunakan kredensial akun administrator. Kredensial ini dapat diperoleh dengan memanfaatkan celah keamanan lain, seperti SQL Injection, dengan *payload* `' or 1=1--` atau `admin@juice-sh.op` dengan password `admin123`.


*Gambar 2: Halaman login diisi dengan payload untuk masuk sebagai admin.*

<img width="632" height="832" alt="image" src="https://github.com/user-attachments/assets/22ff439e-6a1a-4da7-932b-3ed171e2ca7b" />

---

### 3. Mengakses Halaman Admin

Setelah berhasil login sebagai admin, kita mendapatkan hak akses yang diperlukan.

- **Akses Berhasil**: Kembali mengunjungi path `/administration`. Kali ini, halaman dasbor administratif akan berhasil ditampilkan, yang menandakan tantangan telah selesai.


*Gambar 3: Halaman administrasi berhasil diakses setelah login sebagai admin.*

<img width="2042" height="1341" alt="image" src="https://github.com/user-attachments/assets/3b84d4bd-65ec-4e0b-a16d-958efd3200c6" />

---

## Penjelasan Solusi

Tantangan ini diselesaikan dengan **menemukan path administratif yang tersembunyi** dan kemudian **mengaksesnya menggunakan kredensial administrator**. Kerentanan ini terjadi karena keamanan halaman sensitif hanya mengandalkan kerahasiaan URL-nya (*security through obscurity*) tanpa adanya validasi peran pengguna yang kuat di sisi server untuk setiap permintaan.

---

## Rekomendasi Perbaikan (Remediasi)

Untuk mengamankan bagian admin secara efektif, pertimbangkan untuk menerapkan hal-hal berikut:

- **Kontrol Akses yang Tepat**: Pastikan ada mekanisme kontrol akses yang kuat di sisi server. Setiap kali halaman admin diminta, server harus memverifikasi apakah sesi pengguna yang aktif memiliki peran sebagai administrator.
- **Pemisahan Fungsi**: Idealnya, panel admin di-hosting di domain atau server yang berbeda dan tidak dapat diakses dari internet publik untuk membatasi paparan terhadap serangan.
- **Gunakan Web Application Firewall (WAF)**: Terapkan WAF untuk memantau dan memblokir upaya tidak sah untuk mengakses area terlarang atau tersembunyi.
