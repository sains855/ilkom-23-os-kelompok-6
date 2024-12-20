# Deploy Laravel pada Docker Compose
Dokumentasi ini menjelaskan langkah-langkah untuk melakukan deploy aplikasi Laravel menggunakan Docker Compose.
Langkah-Langkah Membuat Laravel Service:
 1. [Cek Status Docker](#1-Cek-Status-Docker)
 2. [Clone Aplikasi Projek ke Server](#2-Clone-Aplikasi-Projek-ke-Server)
 3. [Buat File docker-compose.yml](#3--Buat-File-docker-compose.yml)
 4. [Buat Konfigurasi Nginx](#4-Buat-Konfigurasi-Nginx)
 5. [Buat File Dockerfile](#5-Buat-File-Dockerfile)
 6. [Buat Container Untuk Menjalankan Aplikasi](#6-Buat-Container-Untuk-Menjalankan-Aplikasi)
 
## 1. Cek Status Docker
Pastikan Docker sudah berjalan di server dengan mengetikkan perintah berikut:
```
sudo systemctl status docker
```
## 2. Clone aplikasi Projek ke Server
Clone project Laravel dari repository publik ke server menggunakan perintah berikut:
```
git clone https://github.com/AyanGYdsti/si_perpus.git
```
Setelah selesai, masuk ke direktori project:
```
cd si-perpus
```
## 3. Buat File docker-compose.yml
File ```docker-compose.yml``` akan digunakan untuk mendefinisikan layanan web server, database, dan aplikasi Laravel.
Buat file ```docker-compose.yml``` dengan perintah:

```
nano docker-compose.yml
```
Masukkan konfigurasi berikut ke dalam file:
```
version: "3.7"
services:
  app:
    build:
      args:
        user: yaya
        uid: 1000
      context: ./
      dockerfile: Dockerfile
    image: si-perpus
    container_name: si-perpus-container
    restart: unless-stopped
    working_dir: /var/www/
    volumes:
      - ./:/var/www
    networks:
      - my_network
  db:
    image: mysql:8.2
    container_name: db-container
    restart: unless-stopped
    environment:
      MYSQL_DATABASE: ${DB_DATABASE}
      MYSQL_ROOT_PASSWORD: ${DB_PASSWORD}
      MYSQL_PASSWORD: ${DB_PASSWORD}
      MYSQL_USER: ${DB_USERNAME}
      SERVICE_TAGS: dev
      SERVICE_NAME: mysql
    volumes:
      - ./docker-compose/mysql:/docker-entrypoint-initdb.d
    networks:
      - my_network
  nginx:
    image: nginx:alpine
    container_name: nginx-container
    restart: unless-stopped
    ports:
      - 8000:80
    volumes:
      - ./:/var/www
      - ./docker-compose/nginx:/etc/nginx/conf.d/
    networks:
      - my_network
networks:
  my_network:
    external: true
    name: my_network
    driver: bridge
```
## 4. Buat Konfigurasi Nginx
Konfigurasi Nginx diperlukan untuk mengarahkan request ke aplikasi Laravel.
Buat direktori untuk file konfigurasi:
```
mkdir -p docker-compose/nginx
```
Buat file config nginx
```
nano docker-compose/nginx/nama-proyek-web.conf
```
lalu masukkan script berikut:
```
server {
    listen 80;
    index index.php index.html;
    error_log  /var/log/nginx/error.log;
    access_log /var/log/nginx/access.log;
    root /var/www/public;
    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass app:9000;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param PATH_INFO $fastcgi_path_info;
    }
    location / {
        try_files $uri $uri/ /index.php?$query_string;
        gzip_static on;
    }
}
```
## 5. Buat File Dockerfile
```Dockerfile``` ini digunakan untuk build aplikasi menjadi sebuah image
buat file Dockerfile dengan perintah berikut:
```
nano Dockerfile
```
lalu masukkan script berikut:
```
FROM php:8.2-fpm
ARG user
ARG uid
RUN apt update && apt install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev
RUN apt clean && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
RUN useradd -G www-data,root -u $uid -d /home/$user $user
RUN mkdir -p /home/$user/.composer && \
    chown -R $user:$user /home/$user
WORKDIR /var/www
USER $user
```
## 6. Buat Container Untuk Menjalankan Aplikasi
Setelah semua file siap, jalankan perintah berikut:
Build aplikasi Laravel menjadi sebuah image:
```
docker-compose build app
```
Jalankan aplikasi Laravel dalam container:
```
docker-compose up -d
```

### Akses Aplikasi di Browser 

http://127.0.0.1:8000/

### Menampilan Status Docker Telah Berjalan
![image](https://github.com/user-attachments/assets/f9634440-069b-43aa-88eb-a75548963f25)

### Hasil akhir aplikasi berjalan di browser:
![image](https://github.com/user-attachments/assets/aacdb225-6ade-4567-9f1b-8f7e3133e4db)

## Melakukan Pembatasan Memory dan CPU

### Melakukan Pembatasan Memory
Limit memory pada si-perpus-container
```
 docker update --memory=512m --memory-swap=1g si-perpus-container
```
gunakan Perintah ```docker stats``` digunakan untuk menampilkan statistik penggunaan sumber daya (seperti CPU, memori, disk, dan I/O jaringan) dari container yang sedang berjalan.

![image](https://github.com/user-attachments/assets/5a2e9515-3b23-42e2-8e14-526c20fdd22a)

### Melakukan Pembatasan CPU
Limit  CPU pada si-perpus-container
```
docker update --cpus="1.5" af2dec0cfe9b
```
![image](https://github.com/user-attachments/assets/e8f97e9b-b3c7-498b-8eb7-a2962d836477)

