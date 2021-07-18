# PHP + Apache
FROM php:8.0-apache

# Update OS and install common dev tools
RUN apt-get update && apt-get install -y git unzip zip

# Enable common Apache modules
RUN a2enmod headers expires rewrite

# Set working directory
WORKDIR /var/www

# Using the PHP Extension Installer, install useful plugins
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/
RUN install-php-extensions bcmath intl mbstring mysqli pcntl pdo_mysql soap sockets zip gd xsl opcache

# Install Composer
COPY --from=composer:2.0 /usr/bin/composer /usr/local/bin/composer