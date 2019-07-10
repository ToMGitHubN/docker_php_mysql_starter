FROM php:7-fpm

ADD php.ini /usr/local/etc/php/conf.d/php.ini

RUN apt-get update \
  && apt-get install -y zlib1g-dev libicu-dev g++ \
  && docker-php-ext-configure intl \
  && docker-php-ext-install pdo_mysql mysqli mbstring intl zip

RUN pecl install xdebug \
  && docker-php-ext-enable xdebug

RUN docker-php-ext-install bcmath

RUN apt-get install -y zip unzip


# install composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer
