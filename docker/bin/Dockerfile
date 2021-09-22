FROM php:7.4.23-apache-buster

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get -y update --fix-missing
RUN apt-get upgrade -y
RUN apt-get --no-install-recommends install -y apt-utils
RUN apt-get -y --no-install-recommends install nano zlib1g-dev libzip-dev libicu-dev
RUN apt-get -y --no-install-recommends install --fix-missing apt-utils build-essential curl libonig-dev
RUN apt-get -y --no-install-recommends install --fix-missing libcurl4 libcurl4-openssl-dev zip openssl
RUN apt-get -y --no-install-recommends install --fix-missing libmagickwand-dev \
    && pecl install imagick \
    && docker-php-ext-enable imagick

# composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# PHP extensions
RUN docker-php-ext-install curl && \
    docker-php-ext-install tokenizer && \
    docker-php-ext-install json && \
    docker-php-ext-install zip && \
    docker-php-ext-install -j$(nproc) intl && \
    docker-php-ext-install mbstring && \
    docker-php-ext-install gettext && \
    docker-php-ext-install calendar && \
    docker-php-ext-install exif

RUN apt-get --no-install-recommends install -y libjpeg62-turbo-dev libpng-dev \
    && docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd

# Enable apache modules
RUN a2enmod rewrite headers

RUN rm -rf /var/lib/apt/lists/* && rm -rf /usr/src/*


