# Deploy Laravel pada Docker Compose
Berikut adalah cara untuk deploy aplikasi laravel Anda menggunakan Docker.
Langkah-Langkah Membuat Laravel Service
 1. [Cek Status Docker](#1-Cek-Status-Docker)
 2. [Clone Aplikasi Projek ke Server](#2-Clone-Aplikasi-Projek-ke-Server)
 3. [Buat File docker-compose.yml](#3--Buat-File-docker-compose.yml)
 4. [Buat Konfigurasi Nginx](#4-Buat-Konfigurasi-Nginx)
 5. [Buat File Dockerfile](#5-Buat-File-Dockerfile)
 6. [Buat Container Untuk Menjalankan Aplikasi](#6-Buat-Container-Untuk-Menjalankan-Aplikasi)
 
## 1. Cek Status Docker
Pastikan Docker sudah running dengan mengetikan perintah berikut: 
```
sudo systemctl status docker
```
## 2. Clone splikasi Projek ke Server
Clone project yang ada di public repository ke server dengan perintah berikut:
```
git clone https://github.com/AyanGYdsti/si_perpus.git
```
setelah selesai clone, selanjutnya masuk ke direktori project
```
cd si-perpus
```
## 3. Buat File docker-compose.yml
Selanjutnya kita akan membuat service web server, database, dan aplikasi.
jalankan perintah berikut untuk membuat file docker-compose.yml
```
nano docker-compose.yml
```
lalu masukan script berikut:
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
Selanjutnya buat file konfigurasi Nginx.
Ketikan perintah berikut untuk membuat direktori tempat file config
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
Dockerfile ini digunakan untuk build aplikasi menjadi sebuah image
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
Ketikan perintah berikut untuk build aplikasi menjadi image
```
docker-compose build app
```
Selanjutnya lakukan docker-compose untuk menjalankan image menjadi container 
```
docker-compose up -d
```
