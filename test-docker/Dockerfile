# Gunakan image PHP resmi
FROM php:8.1-apache

# Install dependencies (misalnya, jika menggunakan ekstensi tertentu)
RUN docker-php-ext-install mysqli pdo pdo_mysql

# Salin file PHP Anda ke dalam kontainer
COPY . /var/www/html/

# Expose port 80
EXPOSE 80
