FROM php:8.0-fpm-alpine

LABEL maintainer="Bui Thanh Liem (liem04@gmail.com)"

COPY composer.json /var/www/html/

# Set working directory
WORKDIR /var/www/html

ENV BUILD_DEPS \
    autoconf \
    openssl-dev \
    libressl-dev \
    build-base \
    git \
    pcre-dev \
    freetype \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng \
    libpng-dev \
    gettext-dev \
    libmcrypt-dev \
    libxml2-dev \
    libxslt-dev \
    curl \
    freetype-dev \
    g++ \
    icu \
    icu-dev \
    shadow \
    supervisor \
    bash \
    libzip-dev \
    zlib-dev

RUN rm -rf /var/cache/apk/* && \
    rm -rf /tmp/*

RUN apk update

RUN apk --update --no-cache --virtual .build-deps add ${BUILD_DEPS}

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

#PHPUNIT
RUN composer global require "phpunit/phpunit"

ENV PATH /root/.composer/vendor/bin:$PATH

RUN ln -s /root/.composer/vendor/bin/phpunit /usr/bin/phpunit

# Add UID '1000' to www-data
RUN usermod -u 1000 www-data

# Chang app directory permission
RUN chown -R www-data:www-data .

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]
