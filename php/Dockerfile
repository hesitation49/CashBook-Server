# ベースイメージを指定
FROM php:8.2.0alpha1-fpm-alpine

# PHP設定ファイルを設置
COPY ./php.ini /usr/local/etc/php/php.ini

# `apk`のアップデート、gitなどのツールをインストール
RUN apk --no-cache update \
    && apk --no-cache upgrade \
    && apk --no-cache add icu-dev zlib-dev libzip-dev mariadb mariadb-client vim

# PHP拡張ライブラリのインストール
RUN docker-php-ext-install intl zip pdo pdo_mysql mysqli

# PHP拡張用モジュールの設定 GDのfreetypeとjpegを有効 \
RUN docker-php-ext-configure intl \
    && docker-php-ext-enable intl

# Composerをインストール
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www
