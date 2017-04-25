FROM php:7.1.3-fpm

# Install env && deployed
ADD sources.list    /etc/apt/sources.list
RUN apt-get update && apt-get install -y \
        libmemcached-dev \
        libmcrypt-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng12-dev \
        curl \
        libcurl4-openssl-dev \
        libxml2  libxml2* \
        libpng12-dev \
        && rm -r /var/lib/apt/lists/*


# Install PHP extensions
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) iconv gd curl mbstring xml json mcrypt mysqli pdo pdo_mysql zip
RUN pecl install memcached \
        && pecl install redis \
        && pecl install xdebug \
        # && pecl install amqp \
        && docker-php-ext-enable redis memcached xdebug

# PHP config
ADD php.ini    /usr/local/etc/php/php.ini
ADD php-fpm.conf    /usr/local/etc/php-fpm.conf

# composer
# ADD composer.phar /usr/local/bin/composer
# RUN chmod +x /usr/local/bin/composer \
#     && composer config -g repo.packagist composer https://packagist.phpcomposer.com \
#     && composer self-update \
#     && curl -o /usr/local/bin/phpunit https://phar.phpunit.de/phpunit.phar \
#     && chmod +x /usr/local/bin/phpunit

WORKDIR /opt

# Write Permission
RUN usermod -u 1000 www-data

EXPOSE 9000
VOLUME ["/opt"]