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

# Expose port 80 untuk Apache
EXPOSE 80
```
4. Buat satu folder bernama php, lalu masuk ke dalamnya dan buat satu file bernama index.php.
5. Masukkan syntax php ke dalam file tersebut, contohnya "Hello World".
6. Kembali ke direktori sebelumnya yang telah anda buat.
