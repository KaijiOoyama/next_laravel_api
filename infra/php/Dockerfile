# 公式のphpイメージ
FROM php:8.1-fpm-buster

ENV COMPOSER_ALLOW_SUPERUSER=1 \
    COMPOSER_HOME=/composer

# composerイメージを新たにビルドしcomposer containerからファイルをコピー
COPY --from=composer:2.2 /usr/bin/composer /usr/bin/composer

# aptはcli向きでないという警告が出るためapt-get
RUN apt-get update && \
    # laravelに必要なパッケージ群
    apt-get -y install --no-install-recommends git unzip libzip-dev libicu-dev libonig-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    git clone https://github.com/phpredis/phpredis.git /usr/src/php/ext/redis && \
    # docker-php-ext-install:ｐｈｐのdockerイメージ専用の拡張モジュールのマネージャ
    docker-php-ext-install intl pdo_mysql zip bcmath redis && \
    pecl install xdebug && \
    docker-php-ext-enable xdebug

COPY ./php.ini /usr/local/etc/php/php.ini

WORKDIR /data
