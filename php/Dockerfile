FROM php:7.1.9-fpm
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    curl \
    libicu-dev \
    libmemcached-dev \
    libz-dev \
    libpq-dev \
    libjpeg-dev \
    libpng-dev \
    libfreetype6-dev \
    libssl-dev \
    libmcrypt-dev \
    libxml2-dev \
    libbz2-dev \
    libjpeg62-turbo-dev \
    curl \
    git \
    subversion \
  && rm -rf /var/lib/apt/lists/*
  # Install various PHP extensions
RUN docker-php-ext-configure bcmath --enable-bcmath \
    && docker-php-ext-configure pcntl --enable-pcntl \
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql \
    && docker-php-ext-configure pdo_pgsql --with-pgsql \
    && docker-php-ext-configure mbstring --enable-mbstring \
    && docker-php-ext-configure soap --enable-soap \
    && docker-php-ext-install \
        bcmath \
        intl \
        mbstring \
        mcrypt \
        mysqli \
        pcntl \
        pdo_mysql \
        pdo_pgsql \
        soap \
        sockets \
        zip \
  && docker-php-ext-configure gd \
    --enable-gd-native-ttf \
    --with-jpeg-dir=/usr/lib \
    --with-freetype-dir=/usr/include/freetype2 && \
    docker-php-ext-install gd \
  && docker-php-ext-install opcache \
  && docker-php-ext-enable opcache

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
WORKDIR /ci
COPY . /ci
RUN composer clear-cache
RUN composer dump-autoload
RUN composer install