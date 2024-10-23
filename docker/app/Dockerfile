FROM php:8.1-apache

# PHP 設定ファイル
COPY /docker/app/php.ini /usr/local/etc/php/php.ini

# PHP拡張機能のインストール
RUN apt-get update && apt-get install -y \
    libzip-dev \
    unzip \
    p7zip-full \
    libpq-dev \
    && docker-php-ext-install zip \
    && docker-php-ext-install pdo pdo_mysql

# Apacheモジュールの有効化
RUN a2enmod rewrite

# Set the working directory for Apache
WORKDIR /var/www/html

# Copy composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Install npm for React/Vite
RUN apt-get install -y npm

# タイムゾーン設定
RUN ln -sf  /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# Expose port
EXPOSE 80
