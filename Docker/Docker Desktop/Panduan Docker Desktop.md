### 1. Membuka Docker Desktop
- Jalankan **Docker Desktop** pada komputer Anda.

### 2. Membangun Image
1. Buat satu folder untuk menyimpan file Dockerfile dan file index.
2. Masuk ke dalam folder tersebut, kemudian buat file Dockerfile.
3. Masukkan perintah berikut ke dalam file Dockerfile.
```dockerfile
# Gunakan PHP 8.2 dengan Apache
FROM php:8.2-apache

# Salin file PHP ke direktori yang sesuai di dalam container
COPY ./php /var/www/html

# Install nano
RUN apt update && apt install nano -y

# Expose port 80 untuk Apache
EXPOSE 80
```
4. Buat satu folder bernama php, lalu masuk ke dalamnya dan buat satu file bernama index.php.
5. Masukkan syntax php ke dalam file tersebut, contohnya "Hello World".
6. Kembali ke direktori sebelumnya yang telah anda buat.
7. Lakukan Perintah berikut untuk membuild image.
```bash
docker build -t nama-image .
```
Berikut contoh gambarnya
![Deskripsi Gambar](https://drive.google.com/uc?id=1hVu0TjS1xypN2BqXSjA8Ntk9ikpB2n2B)
8. Image sudah terbuild, selanjutnya lanjut untuk menjalankan container dari image yang sudah ada dengan Docker Desktop

### 3. Menjalankan Docker Image
1. Buka **Docker Desktop** dan masuk ke tab **Images**.
2. Pastikan image yang akan digunakan sudah tersedia.
3. Cari image yang ingin dijalankan pada daftar yang tersedia.
4. Klik tombol **Run** pada image tersebut.
5. Konfigurasikan pengaturan berikut di dialog yang muncul:
   - **Container Name**: Masukkan nama untuk container.
   - **Ports**: Tentukan port yang akan digunakan, seperti `8080:80`.
   - **Optional Settings**: Atur opsi tambahan seperti volume atau environment variable jika diperlukan.
   6. Klik **Run** untuk memulai container.
   ![Deskripsi Gambar](https://drive.google.com/uc?id=1bFhYinGrG4fNUiXQzC8WvnTjhFn9yGK1)

### 4. Periksa Apakah Container Sudah Berjalan Pada Tab Container
1. Jika sudah berjalan icon kolom action akan berbentuk kotak
   ![Gambar dari Google Drive](https://drive.google.com/uc?id=1HoSK3q1-PJIfawhGrFGs0nWGpAnnkPm_)

### 5. Jika Sudah Berjalan Kunjungi Port Sesuai Dengan Container Yang Ada
1. Jika website berhasil terbuka artinya container berjalan tanpa error.
Output Web:
   ![Gambar dari Google Drive](https://drive.google.com/uc?id=1je6n2V0eSlsqPRYPIrdC3zJ5FvbiArJE)