# Docker推奨OS
FROM debian:stretch-slim

# MAINTAINER は非推奨なので、LABELを使用。
LABEL maintainer="haruka-kawanaka@cafu0402"

# パッケージのインストール

## プリインストールしておきたいパッケージを登録する
ENV PRE_INSTALLS \
    tree \
    vim

# PHP7.3 を LAMP環境で使用するために必要なOSのモジュール軍
# 参考 https://def-4.com/debian-stretch-php73/
ENV WEBSERVER_MODULES \
    apt-transport-https \
    lsb-release \
    ca-certificates \
    wget

RUN apt-get update && apt-get install -y \
    $PRE_INSTALLS \
    $WEBSERVER_MODULES

RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'

# PHP7.3 モジュール
ENV PHP73_MODULES \
    php7.3 \
    php7.3-fpm \
    php7.3-mysql \
    php7.3-mbstring \
    php7.3-xml \
    php7.3-gd \
    php7.3-curl \
    php7.3-mysqli
# PHP7.3のモジュールとApache2のインストール
RUN apt-get update && apt-get -y install \
    $PHP73_MODULES \
    apache2

