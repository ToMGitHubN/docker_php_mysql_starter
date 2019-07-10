# [START dockerfile]
FROM php:7.3-apache-stretch

# install PHP拡張モジュール + vim
RUN apt-get update \
	&& apt-get upgrade -y
RUN apt-get install -y libwebp-dev libjpeg-dev libpng-dev libicu-dev libxml2-dev libxslt1-dev zlib1g-dev libzip-dev libpq-dev g++ \
	&& apt-get install -y git vim \
	&& docker-php-ext-install zip pdo_mysql mysqli mbstring \
    && apt-get clean


# mod_rewrite ON
RUN a2enmod rewrite

# DOCUMENT_ROOT change
#Basc認証
ENV APACHE_DOCUMENT_ROOT=/var/www/html/public
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf \
    && sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf
#    && sed -i -e '$a <Location />\nAuthType Basic\nAuthName "Basic Auth"\nAuthUserFile /var/www/html/.htpasswd\nRequire valid-user\n</Location>' /etc/apache2/apache2.conf


# LANGUAGE "ja_JP.UTF-8"
RUN apt-get install -y locales \
	&& apt-get clean \
	&& locale-gen ja_JP.UTF-8 \
	&& localedef -f UTF-8 -i ja_JP ja_JP
ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:jp
ENV LC_ALL ja_JP.UTF-8

# TIME ZONE "Asia/Tokyo"
ENV TZ=Asia/Tokyo

# install composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer

# setup yarn & node
RUN curl -sL https://deb.nodesource.com/setup_11.x | bash - \
    && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
	&& apt-get update \
	&& apt-get install -y nodejs yarn \
	&& apt-get remove cmdtest \
	&& apt-get clean \
	&& mkdir /var/www/.yarn \
    && mkdir /var/www/.config \
    && chown www-data:www-data /var/www/.yarn \
    && chown www-data:www-data /var/www/.config



# [END dockerfile]
