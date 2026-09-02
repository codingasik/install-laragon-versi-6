# Panduan Setup & Upgrade Environment Laragon 6 (Laravel 13 Ready)

Repository ini berisi panduan dan file konfigurasi `packages.conf` untuk menyelaraskan versi **PHP, Apache, MySQL, dan phpMyAdmin** di Laragon kamu agar 100% identik dengan environment yang digunakan pada Ebook.

> **Catatan:** Panduan ini diperuntukkan bagi kamu yang menggunakan **Laragon versi lama V6**. Jika kamu sudah menginstal Laragon versi terbaru atau menggunakan stack lain (seperti XAMPP) yang versi komponennya sudah baru, kamu bisa mengabaikan langkah upgrade ini.

Jika mau unduh versi lama 6 kamu bisa juga unduh di : https://drive.google.com/file/d/1_PLnKFXIcjvbAhkvba8kHJTLWoxZBmuf/view?usp=sharing

---

## Spesifikasi Environment

* **PHP:** 8.5.10
* **Apache:** 2.4.68
* **MySQL:** 26.7.0
* **phpMyAdmin:** 5.2.3
* **composer:** 2.10.3

---

## 🛑 PENTING: Langkah Keamanan Database (BACA DULU!)

Sebelum melakukan upgrade versi MySQL, **AMANKAN DATABASE LAMA KALIAN** agar tidak hilang/tertimpa!

1. Buka folder instalasi Laragon kamu, lalu masuk ke folder data:
   `C:\laragon\data\`
2. Kamu akan melihat folder `mysql` (atau `mysql-8.0.x`).
3. **Copy dan Backup** folder tersebut ke tempat aman (misalnya ke Desktop) sebagai cadangan.
4. *Penjelasan:* Menambah atau mengganti versi MySQL baru tidak akan menghapus folder data lama secara otomatis, namun melakukan backup fisik wajib dilakukan untuk menghindari kesalahan pemindahan folder.

---

## Cara Upgrade Environment di Laragon

### Langkah 1: Replace File `packages.conf`

1. Unduh file `packages.conf` dari repository ini.
2. Buka folder `C:\laragon\usr\` di komputer kamu.
3. *Replace* (timpa) file `packages.conf` bawaan dengan file baru yang sudah diunduh.

---

### Langkah 2: Unduh Komponen via Quick Add

1. Jalankan aplikasi Laragon.
2. Klik kanan di mana saja pada jendela Laragon.
3. Pilih **Tools** > **Quick add**.
4. Klik dan install satu persatu komponen berikut:
   * **PHP 8.5.10**
   * **Apache 2.4.68**
   * **MySQL 26.7.0**
   * **phpMyAdmin 5.2.3**
   * **composer 2.10.3**
5. Tunggu hingga proses pengunduhan dan ekstraksi otomatis selesai.

---

### Langkah 3: Mengubah Versi yang Aktif di Laragon

Setelah proses pengunduhan selesai, kamu perlu mengaktifkan versi baru tersebut:

1. **Ubah Versi PHP:**
   * Klik kanan Laragon > **PHP** > **Version** > Pilih `8.5.10`.
2. **Ubah Versi Apache:**
   * Klik kanan Laragon > **Apache** > **Version** > Pilih `2.4.68`.
3. **Ubah Versi MySQL:**
   * Klik kanan Laragon > **MySQL** > **Version** > Pilih `26.7.0`.

---

### Langkah 4: Konfigurasi Apache (`httpd.conf`)

Agar modul SSL pada Apache versi 2.4.68 berjalan normal, lakukan konfigurasi berikut:

#### Opsi A: Edit Manual (Direkomendasikan)
1. Pastikan Apache sudah beralih ke versi `2.4.68`.
2. Klik kanan Laragon > **Apache** > pilih **httpd.conf**.
3. Cari dua baris berikut (gunakan `Ctrl + F`):
   ```apache
   #LoadModule ssl_module modules/mod_ssl.so
   #LoadModule socache_shmcb_module modules/mod_socache_shmcb.so
   
4. Hapus tanda # di depan kedua baris tersebut (uncomment) sehingga menjadi:
	LoadModule ssl_module modules/mod_ssl.so
	LoadModule socache_shmcb_module modules/mod_socache_shmcb.so
	
5. Simpan (Ctrl + S) file tersebut.

#### Opsi B: Replace File Direct
Kamu juga bisa langsung menimpa file httpd.conf yang ada di:
C:\laragon\bin\apache\httpd-2.4.68-260827-Win64-VS18\conf\httpd.conf
menggunakan file httpd.conf yang sudah disediakan di repository ini.

---

### Langkah 5: Pindahkan Database Lama ke MySQL Baru (Jika Ada)

Jika kamu ingin menggunakan database yang dibuat di MySQL versi lama pada MySQL 26.7.0:

1. Stop servis Laragon terlebih dahulu (Stop All).
2. Buka folder C:\laragon\data\.
3. Salin (copy) folder-folder nama database kamu dari folder mysql lama ke folder mysql-26.7.0 yang baru terbuat.
4. Jalankan kembali servis Laragon (Start All).

---

### Langkah 6: Tambahkan PHP, Mysql dan Composer ke Environment Variable di Windows

Ini untuk pengguna windows tentunya, OS lainnya disesuaikan saja. Dan jika sudah ada di env windows, abaikan saja step ini

1. Buka tab pencarian windows, cari "env" tanpa tanda petik
2. Pilih Edit the system environment variables
3. Ke tab Advanced dan pilih Environment Variables
4. Di tab System variables dibawah, pilih PATH dan klik tab
5. Jika belum ada path mysql, tambahkan ini dengan klik New dan isi dengan : "C:\laragon\bin\mysql\mysql-26.7.0-winx64\bin" tanpa petik
6. Tambahkan lagi jika belum ada php dengan versimu misal versi 8.5.10 : "C:\laragon\bin\php\php-8.5.10-Win32-vs17-x64" tanpa petik
7. Tambahkan juga jika belum ada composer dengan : "C:\laragon\bin\composer" tanpa petik. Tapi pastikan sudah install composer via Laragon
8. Setelah itu klik ok semua dan coba buka cmd dan cek versi php dan mysql
9. Ketik "php -version" tanpa petik. Harusnya muncul versi PHP misal 8.5.19
10. Ketik lagi "mysql -version" tanpa petik. Harusnya juga muncul versi Mysql misal 26.7.0
11. Jika sudah maka berhasil


---

### Final Check

Setelah semua langkah dilakukan:

1. Restart Laragon (Stop All lalu Start All).
2. Buka Terminal Laragon / CMD, jalankan:
3. php -v (Pastikan memuat PHP 8.5.10)
4. mysql --version (Pastikan memuat MySQL 26.7.0)
5. Akses http://localhost/phpmyadmin melalui browser untuk memastikan dashboard phpMyAdmin dapat terbuka tanpa kendala.

Selamat! Environment Laragon kamu sudah 100% siap untuk menjalankan proyek Laravel 13 di Ebook ini.