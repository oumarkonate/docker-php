FROM php:7.3-fpm-stretch

RUN apt-get update && apt-get install -y \
    git \
    curl \
    libxml2-dev \
    libpng-dev \
    libjpeg62-turbo-dev \
    jpegoptim \
    pngquant \
    openssh-client \
    libwebp-dev \
    unzip \
    zip \
    debconf-utils \
    locales \
    zlib1g-dev \
    libicu-dev \
    librabbitmq-dev

RUN docker-php-ext-configure gd --with-png-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-webp-dir=/usr/include/

RUN docker-php-ext-configure intl

RUN docker-php-ext-install -j$(nproc) pdo_mysql xml bcmath mbstring iconv gd intl opcache

RUN pecl install amqp
RUN docker-php-ext-enable amqp

ENV PHPREDIS_VERSION 3.0.0

RUN echo "memory_limit = 512M\ndate.timezone = Europe/Paris" > /usr/local/etc/php/conf.d/memory-limit.ini

RUN mkdir -p /usr/src/php/ext/redis \
    && curl -L https://github.com/phpredis/phpredis/archive/$PHPREDIS_VERSION.tar.gz | tar xvz -C /usr/src/php/ext/redis --strip 1 \
    && echo 'redis' >> /usr/src/php-available-exts \
    && docker-php-ext-install -j$(nproc) redis

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer --version=1.10.16 && \
    php -r "unlink('composer-setup.php');"

RUN echo "Europe/Paris" > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata

RUN echo "locales locales/default_environment_locale select fr_FR.UTF-8" | debconf-set-selections \
    && echo "locales locales/locales_to_be_generated multiselect 'fr_FR.UTF-8 UTF-8'" | debconf-set-selections

RUN echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen \
    && locale-gen fr_FR.UTF-8 \
    && dpkg-reconfigure -f noninteractive locales \
    && mkdir -p /space/datanfs/yatta/yattacms/storage/audio \
    /space/datanfs/yatta/yattacms/storage/export \
    /space/datanfs/yatta/yattacms/storage/image

EXPOSE 8080
EXPOSE 8081
