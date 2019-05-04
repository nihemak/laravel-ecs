FROM php:7.3.4-fpm

ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NOWARNINGS yes

RUN apt-get update \
    && apt-get install -y libzip-dev \
    && docker-php-ext-install zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

RUN mkdir -p /app
ADD ./laravel/ /app/

WORKDIR /app

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_NO_INTERACTION 1
RUN composer install
RUN cp .env.example .env
RUN php artisan key:generate
RUN chmod -R a+w storage/ bootstrap/cache