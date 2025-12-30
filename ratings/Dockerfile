# Build the app
FROM php:7.4-apache

# IMPORTANT: use a larger temp directory during build
ENV TMPDIR=/var/tmp
ENV MAKEFLAGS="-j1"

RUN apt-get update \
 && apt-get install -yqq unzip libzip-dev \
 && docker-php-ext-install pdo_mysql opcache zip \
 && rm -rf /var/lib/apt/lists/*

# Enable AutoProfile for PHP (Instana)
RUN echo "instana.enable_auto_profile=1" > "/usr/local/etc/php/conf.d/zzz-instana-extras.ini"

# Apache configuration
COPY status.conf /etc/apache2/mods-available/status.conf
RUN a2enmod rewrite && a2enmod status

WORKDIR /var/www/html

COPY html/ /var/www/html

# Install dependencies
COPY --from=composer /usr/bin/composer /usr/bin/composer
RUN composer install

# Permissions (demo-friendly)
RUN rm -rf /var/www/var/* \
 && chown -R www-data:www-data /var/www \
 && chmod -R 777 /var/www

