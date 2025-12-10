FROM php:8.2-fpm

ENV DEBIAN_FRONTEND noninteractive

# 1. Aggiorna il sistema E POI installa le dipendenze (l'ordine è fondamentale)
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    zlib1g-dev \
    curl \
    procps \
    libzip-dev \
    libonig-dev \
    libpng-dev \
    libwebp-dev \
    libjpeg62-turbo-dev \
    libxpm-dev \
    libfreetype6-dev \
    libc-client-dev \
    libkrb5-dev \
    libldap2-dev \
    imagemagick \
    libmagickwand-dev \
    libheif-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp \
    && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
    && docker-php-ext-install -j$(nproc) \
    sockets \
    bcmath \
    pcntl \
    zip \
    mbstring \
    mysqli \
    pdo \
    pdo_mysql \
    opcache \
    ldap \
    gd \
    intl \
    && pecl install imap && docker-php-ext-enable imap \
    && pecl install imagick && docker-php-ext-enable imagick \
    && pecl install redis && docker-php-ext-enable redis \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# 2. Imposta la cartella di lavoro corretta
WORKDIR /code

# 3. Assegna i permessi iniziali
RUN chown -R www-data:www-data /code

# 4. Espone la porta standard di PHP-FPM
EXPOSE 9000
