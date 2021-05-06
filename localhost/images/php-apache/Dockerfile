# PHP + Apache
FROM php:7.3-apache

# Update OS and install common dev tools
RUN apt-get update
RUN apt-get install -y wget vim git zip unzip zlib1g-dev libzip-dev libpng-dev

# Install PHP extensions needed
RUN docker-php-ext-install -j$(nproc) mysqli pdo pdo_mysql gd zip pcntl exif

# Enable common Apache modules
RUN a2enmod headers expires rewrite

# Set working directory to web files
WORKDIR /var/www