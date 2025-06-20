# 🛠️ Maintenance Dokumentation

## 1. Judul Proyek

- **Nama Aplikasi** : WPU Admin – Sistem Manajemen Pengguna  
- **Versi** : 1.0  
- **Repository / URL** : http://localhost/wpu-login  github : https://github.com/Mitamanzila14/wpu-login
- **Nama Penyusun** : Mita Manzila Tusifa  
- **Tanggal Pembuatan Dokumentasi** : 20 Juni 2025

---

## 2. Deskripsi Umum Aplikasi

Aplikasi WPU Admin adalah sistem berbasis web yang digunakan untuk mengelola data pengguna, termasuk fitur tambah, ubah, lihat, dan hapus pengguna. Sistem ini juga membedakan antara admin dan user biasa melalui sistem role-based access control, upload profil pengguna, serta sistem login dan logout dengan validasi sesi.

Aplikasi ini dibangun menggunakan:
- **Bahasa Pemrograman** : PHP
- **Framework** : CodeIgniter 3
- **Database** : MySQL (dikelola melalui phpMyAdmin)
- **Web Server** : Apache (melalui XAMPP)
- **Sistem Operasi Target** : Windows (via XAMPP) atau Linux (via Apache + MySQL)
- **Antarmuka Web** : HTML, CSS, Bootstrap

---

## 3. Struktur Direktori dan File

Struktur direktori aplikasi mengikuti pola standar CodeIgniter 3. Penjelasan masing-masing folder penting:
- `application/controllers/` : Berisi controller seperti Admin.php (mengelola pengguna), Auth.php (mengelola login/logout), dll (sesuai kebutuhan aplikasi). Controller mengatur alur aplikasi.
- `application/models/` : Berisi file model, seperti User_model.php, yang bertanggung jawab atas komunikasi dengan database.
- `application/views/` : Berisi tampilan HTML yang diproses oleh controller, contohnya manageuser.php, edit_user.php, dll.
- `application/config/` : Folder ini menyimpan pengaturan utama seperti koneksi database (database.php), autoload (autoload.php), dan konfigurasi dasar (config.php).
- `assets/` : Berisi file statis yang dibutuhkan antarmuka, seperti gambar, file CSS, dan JavaScript.
- `uploads/` : Folder untuk menyimpan file yang diunggah pengguna, seperti gambar profil.

---

## 4. Instruksi Instalasi dan Konfigurasi

Langkah-langkah untuk menjalankan aplikasi ini di lokal:
1. Salin folder project ke dalam `htdocs`.
2. Buka XAMPP dan jalankan Apache dan MySQL.
3. Buat database di phpMyAdmin, misalnya dengan nama `wpu-login`.
4. Import struktur dan data database dari file .sql yang tersedia.
5. Konfigurasi database di `application/config/database.php`:
```php
$db['default'] = array(
    'hostname' => 'localhost',
    'username' => 'root',
    'password' => '',
    'database' => 'wpu-login',
    ...
);
```
6. Buka `http://localhost/wpu-login` di browser untuk menjalankan aplikasi.

---

## 5. Dependency yang Digunakan

Daftar dependensi teknis yang digunakan:
- CodeIgniter 3: Framework utama PHP, ringan dan cocok untuk aplikasi kecil-menengah.
- Bootstrap: Framework CSS untuk mempercantik tampilan UI.
- jQuery: Library JavaScript untuk keperluan DOM dan event.
- FontAwesome: Ikon antarmuka pengguna.
- phpMyAdmin: Untuk mengelola database MySQL.

**Kompatibilitas Versi:**
- PHP 7.x (CodeIgniter 3 tidak mendukung PHP 8.x penuh).
- Apache 2.4 atau yang kompatibel.
- Tidak memerlukan Composer karena CodeIgniter 3 tidak berbasis dependency modern.

---

## 6. Instruksi Build dan Deployment

**Build**: Tidak ada build seperti di aplikasi modern. Cukup jalankan aplikasi lewat browser setelah setup.

**Deployment ke Hosting**:
- Upload semua file ke `public_html` via cPanel atau FTP.
- Buat database dan import .sql ke hosting (melalui phpMyAdmin).
- Ubah konfigurasi database:
```php
'hostname' => 'localhost',
'username' => 'nama_user_hosting',
'password' => 'password_hosting',
'database' => 'nama_db_hosting',
```
- Ubah `base_url` di `application/config/config.php` menjadi URL hosting:
```php
$config['base_url'] = 'https://domainanda.com/';
```

---

## 7. Panduan Debugging dan Logging

**Debugging:**
- Aktifkan error reporting: `index.php` (set `ENVIRONMENT` ke `development`).
- Gunakan `log_message('error', 'Pesan error');` untuk mencatat kesalahan.

**Logging:**
- Lokasi file log : `application/logs/`
- Format nama file log : `log-2025-06-20.php`
- Level log : error, debug, info
- Contoh penggunaan: `log_message('debug', 'Log ini untuk testing');`

**Tools Pendukung:**
- Chrome DevTools : Cek konsol error HTML/JS.
- phpMyAdmin : Validasi data dan relasi.
- Postman : Jika nanti mengembangkan API backend.

---

## 8. Catatan Perubahan (Change Log)

| Versi | Tanggal      | Perubahan                                        |
|-------|--------------|--------------------------------------------------|
| 1.0.0 | 2025-06-09   | Rilis awal aplikasi dan fitur login              |
| 1.1.0 | 2025-06-11   | Tambah validasi form login dan upload foto      |
| 1.2.0 | 2025-06-15   | Tambah fitur pencarian nama/email               |
| 1.3.0 | 2025-06-18   | Perbaikan bug flashdata tampil di halaman lain |

---

## 9. Bug Dikenal

Bug yang masih belum diperbaiki:

**a. Tidak ada pagination pada daftar pengguna**  
Saat jumlah data pengguna semakin banyak, semua data langsung ditampilkan di satu halaman tanpa pembatas. Hal ini dapat menyebabkan halaman menjadi berat dan tidak efisien.  
_Solusi sementara:_ tambahkan fitur pagination menggunakan query LIMIT dan OFFSET di controller serta menambahkan navigasi halaman di view.

**b. Tampilan tabel belum responsif di layar kecil (mobile)**  
Tampilan tabel daftar pengguna tidak menyesuaikan ukuran layar jika dibuka di perangkat seperti handphone.  
_Solusi sementara:_ bungkus elemen `<table>` dengan `<div class="table-responsive">` agar tabel dapat digeser secara horizontal di layar kecil.

---

## 10. Saran Pengembangan Selanjutnya

a. **Notifikasi email otomatis saat user ditambahkan atau diubah**  
Agar pengguna mendapatkan konfirmasi setelah admin membuatkan akun atau mengubah datanya. Bisa diterapkan menggunakan library Email bawaan CodeIgniter.

b. **Menambahkan fitur pengaturan role secara dinamis**  
Saat ini role mungkin masih bersifat statis. Dengan menambahkan fitur manajemen role (hak akses CRUD), admin bisa membuat peran baru dengan hak akses berbeda tanpa harus ubah kode.

c. **Menerapkan pagination pada tabel daftar user**  
Untuk meringankan tampilan ketika data pengguna sangat banyak. Ini akan meningkatkan efisiensi loading dan pengalaman pengguna.

d. **Tampilan yang lebih responsif dan mobile-friendly**  
Desain tampilan antarmuka sebaiknya disesuaikan dengan berbagai ukuran layar, terutama smartphone. Gunakan class `table-responsive` dan framework seperti Bootstrap 5 untuk optimasi.

e. **Menambahkan fitur filter dan urutkan data pengguna**  
Tambahan tombol sort (urut berdasarkan nama, tanggal, role, dsb) dan filter akan sangat membantu admin mencari data dengan cepat.

f. **Menerapkan sistem CI/CD sederhana jika di-deploy online**  
Jika aplikasi ini dihosting online, gunakan GitHub Actions atau platform lain agar proses upload/update aplikasi otomatis dan terkontrol.

g. **Membuat dokumentasi REST API (jika akan dikembangkan sebagai backend)**  
Dokumentasi API dibutuhkan jika suatu saat aplikasi ini digunakan untuk mobile app atau sistem lain yang membutuhkan integrasi.
