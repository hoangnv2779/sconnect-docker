# Sử dụng image PHP với PHP-FPM
FROM php:8.1-fpm

# Cài đặt các extensions và công cụ cần thiết
RUN apt-get update && apt-get install -y \
    nginx \
    curl \
    git \
    libicu-dev \
    libonig-dev \
    libzip-dev \
    zip \
    unzip \
    && docker-php-ext-install pdo pdo_mysql intl \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && rm -rf /var/lib/apt/lists/*

# Cài đặt Node.js 20 và npm
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - && \
    apt-get install -y nodejs

# Cài đặt Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Copy file cấu hình PHP
COPY php.ini /usr/local/etc/php/

# Copy file cấu hình Nginx
COPY nginx.conf /etc/nginx/nginx.conf

# Copy file vhost cấu hình Nginx
COPY default.conf /etc/nginx/conf.d/default.conf

# Copy source code vào container
WORKDIR /var/www/html

# Expose cổng 80 để Nginx lắng nghe
EXPOSE 80

# Khởi động cả Nginx và PHP-FPM
CMD service nginx start && php-fpm
