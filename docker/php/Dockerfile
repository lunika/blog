FROM php:5.6-apache

RUN apt-get update && apt-get install -y \
 git \
 zip \
 libzip-dev \
 && docker-php-ext-install zip

RUN a2enmod rewrite
RUN usermod -u 1000 www-data
COPY php.ini /usr/local/etc/php/
COPY vhost.conf /etc/apache2/sites-enabled/