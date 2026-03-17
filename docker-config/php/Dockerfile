FROM php:7.4-fpm-alpine
WORKDIR /var/www

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

COPY . /var/www

# Install system packages and PHP extensions needed for Laravel-style apps.
RUN apk add --no-cache \
  git \
  unzip \
  curl \
  gnupg \
  openssl \
  freetype \
  libjpeg-turbo \
  libpng \
  libzip \
  libpq \
  && apk add --no-cache --virtual .build-deps \
  libpng-dev \
  libjpeg-turbo-dev \
  freetype-dev \
  libzip-dev \
  postgresql-dev \
  && docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j"$(nproc)" pdo_mysql mysqli gd zip \
  && apk del --no-cache .build-deps

RUN chown -R www-data:www-data /var/www

# Add php.ini
COPY php.ini /usr/local/etc/php/
