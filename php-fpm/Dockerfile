FROM php:7.2-fpm

ENV TZ=Asia/Shanghai

RUN sed -i "s@http://deb.debian.org@http://mirrors.aliyun.com@g" /etc/apt/sources.list && rm -Rf /var/lib/apt/lists/*

#  更新安装依赖包和PHP核心拓展

RUN apt-get update &&  apt-get upgrade -y && apt-get install -y -f --no-install-recommends apt-utils \
        git \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libcurl4-gnutls-dev \
        libpng-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
        && docker-php-ext-install pdo_mysql \
        && docker-php-ext-install opcache \
        && docker-php-ext-install mysqli \
        && docker-php-ext-install gettext \
        && rm -r /var/lib/apt/lists/*


COPY ./php.ini /usr/local/etc/php/conf.d/php.ini