
# Dokumentasi Proyek Docker PHP

## **1. Persyaratan Sistem**

Sebelum memulai, pastikan Anda telah menginstal Docker dan Docker Compose di sistem Anda.

- **Docker**: [Instalasi Docker](https://docs.docker.com/get-docker/)
- **Docker Compose**: [Instalasi Docker Compose](https://docs.docker.com/compose/install/)

## **2. Masuk ke Direktori `test-docker`**

Pastikan Anda berada di direktori proyek `test-docker`. Gunakan terminal untuk masuk ke dalam direktori ini:

```bash
cd /path/to/your/test-docker
```

## **3. Membangun dan Menjalankan Container dengan Docker Compose**

Jalankan perintah berikut untuk membangun dan menjalankan container menggunakan Docker Compose:

```bash
docker-compose up --build
```

Perintah ini akan membangun image yang diperlukan (jika belum ada) dan menjalankan container berdasarkan konfigurasi yang ada di `docker-compose.yml`.

## **4. Memastikan Web Berjalan**

Setelah menjalankan container, buka browser Anda dan kunjungi alamat berikut untuk memastikan bahwa aplikasi web Anda berjalan dengan baik:

```
http://localhost:8080
```

Jika aplikasi PHP Anda berhasil dijalankan, Anda akan melihat halaman yang diinginkan.
