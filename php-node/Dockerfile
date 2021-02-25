FROM php:7.2.18-fpm

LABEL maintainer="contact@zainoudine-soule.net"
LABEL version="1.0"

RUN apt-get clean
RUN apt-get update

RUN pecl install xdebug-2.6.0 && docker-php-ext-enable xdebug

### PHP extension
RUN apt-get install -y --no-install-recommends \
		libjpeg-dev \
		libmagickwand-dev \
		libpng-dev \
		libzip-dev
## GD
RUN docker-php-ext-configure gd \
    --with-png-dir=/usr/lib \
    --with-jpeg-dir=/usr/lib \
    --with-gd
RUN docker-php-ext-install gd

RUN docker-php-ext-install bcmath exif mysqli opcache

## ZIP
RUN apt-get install -y zip libzip-dev
RUN docker-php-ext-configure zip --with-libzip
RUN docker-php-ext-install zip

## Imagick
RUN apt-get install -y libmagickwand-dev
RUN pecl install imagick
RUN docker-php-ext-enable imagick


### Node

RUN curl -fsSL https://deb.nodesource.com/setup_15.x | bash -
RUN apt-get install -y nodejs

### Tools

## composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN rm composer-setup.php

## WP CLI
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
RUN chmod +x wp-cli.phar
RUN mv wp-cli.phar /usr/local/bin/wp

## Git
RUN apt-get update
RUN apt-get install -y git

## nano
RUN apt-get install nano

RUN apt-get -qy autoremove

EXPOSE 9000
CMD ["php-fpm"]
