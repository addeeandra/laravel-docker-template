FROM php:7.4-apache

RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libzip-dev \
    imagemagick \
    libmcrypt-dev \
    libpng-dev \
    libpq-dev \
    libxrender1 \
    locales \
    openssh-client \
    patch \
    unzip \
    zlib1g-dev \
    zip \
    --no-install-recommends && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install \
    gd \
    bcmath \
    pcntl \
    pdo \
    pdo_pgsql \
    pdo_mysql \
    zip

RUN docker-php-ext-configure gd

RUN cp /usr/share/i18n/SUPPORTED /etc/locale.gen
RUN locale-gen

COPY 000-default.conf /etc/apache2/sites-available/
RUN a2enmod rewrite

COPY --from=composer:1.10 /usr/bin/composer /usr/bin/composer
