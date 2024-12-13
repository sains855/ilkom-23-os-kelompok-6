# Gunakan PHP 8.2 dengan Apache
FROM php:8.2-apache

# Salin file PHP ke direktori yang sesuai di dalam container
COPY ./php /var/www/html

# Install nano
RUN apt update && apt install nano -y

# Expose port 80 untuk Apache
EXPOSE 80