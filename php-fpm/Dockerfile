FROM php:7.2-fpm

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN echo 'Asia/Shanghai' >/etc/timezone

ADD sources.list /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \

    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install bcmath zip opcache iconv  pdo pdo_mysql mysqli

RUN apt-get install -y libmcrypt-dev \
    && pecl install mcrypt-1.0.1  \
    && docker-php-ext-enable mcrypt

RUN pecl install redis-4.0.1 \
    && pecl install xdebug-2.6.0 \
    && docker-php-ext-enable redis xdebug

ADD php.ini /usr/local/etc/php/php.ini



