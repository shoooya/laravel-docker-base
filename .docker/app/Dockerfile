FROM php:8.2-fpm

ENV TZ=Asia/Tokyo

COPY --from=composer:2.5 /usr/bin/composer /usr/bin/composer

# php conf
COPY ./php.ini /etc/php.ini
COPY ./www.conf /etc/php-fpm.d/www.conf

RUN apt-get update \
  && apt-get install -y git unzip\
  && docker-php-ext-install pdo_mysql
