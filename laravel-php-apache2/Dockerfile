
##
##  use php apache 
##

FROM php:7.2-apache

RUN apt-get update


RUN apt-get install -y git zip curl sudo unzip
RUN apt-get install -y libicu-dev libbz2-dev libpng-dev libjpeg-dev libmcrypt-dev libreadline-dev libfreetype6-dev g++


COPY --from=composer:latest /usr/bin/composer /usr/bin/composer


# 3. mod_rewrite for URL rewrite and mod_headers for .htaccess extra headers like Access-Control-Allow-Origin-
RUN a2enmod rewrite headers
RUN echo "ServerTokens Prod" >> /etc/apache2/apache2.conf
RUN echo "ServerSignature Off" >> /etc/apache2/apache2.conf



#COPY host.conf /etc/apache2/sites-available/000-default.conf



# 4. start with base php config, then add extensions
#RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

RUN docker-php-ext-install gd
RUN docker-php-ext-install bz2

RUN docker-php-ext-install intl
RUN docker-php-ext-install iconv
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install sockets
RUN docker-php-ext-install opcache
RUN docker-php-ext-install calendar

RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install exif

#RUN docker-php-ext-install zip
#RUN docker-php-ext-install mbstring

ENV APACHE_DOCUMENT_ROOT=/var/www/html/public

RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf


RUN service apache2 restart

