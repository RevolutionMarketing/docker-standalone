FROM php:8.2-fpm

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    git unzip cron procps zlib1g-dev curl \
    libzip-dev libonig-dev libpng-dev libwebp-dev \
    libjpeg62-turbo-dev libxpm-dev libfreetype6-dev \
    libc-client-dev libkrb5-dev libldap2-dev \
    imagemagick libmagickwand-dev libheif-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp \
    && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
    && docker-php-ext-install -j$(nproc) \
        sockets bcmath pcntl zip mbstring mysqli pdo pdo_mysql opcache ldap gd intl \
    && pecl install redis && docker-php-ext-enable redis \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /code
