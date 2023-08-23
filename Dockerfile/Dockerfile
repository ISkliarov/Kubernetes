# Use an official PHP runtime as the base image
FROM php:7.4-apache

# Set environment variables for PHP
ENV PHP_INI_DIR /usr/local/etc/php
ENV APACHE_DOCUMENT_ROOT /var/www/html

# Enable Apache's mod_rewrite for URL rewriting
RUN a2enmod rewrite

# Install additional PHP extensions and system dependencies as needed
RUN apt-get update && apt-get install -y \
  libpng-dev \
  libjpeg-dev \
  libfreetype6-dev \
  && docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j$(nproc) gd mysqli pdo pdo_mysql

# Copy your PHP application files into the Apache document root
COPY ./index.php /var/www/html

# Expose port 80 to the outside world
EXPOSE 80

# Start Apache when the container launches
CMD ["apache2-foreground"]