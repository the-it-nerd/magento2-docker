FROM php:8.1-fpm-buster
MAINTAINER Raul Sakai <rqsakai@gmail.com>

ARG APP_ID=1000
RUN groupadd -g "$APP_ID" app \
  && useradd -g "$APP_ID" -u "$APP_ID" -d /var/www -s /bin/bash app


RUN mkdir -p /etc/nginx/html /var/www/html /sock \
  && chown -R app:app /etc/nginx /var/www /usr/local/etc/php/conf.d /sock

RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash -

RUN apt-get update && apt-get install -y \
    cron \
    default-mysql-client \
    git \
    gnupg \
    gzip \
    libbz2-dev \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libmagickwand-dev \
    libmcrypt-dev \
    libonig-dev \
    libpng-dev \
    libsodium-dev \
    libssh2-1-dev \
    libwebp-dev \
    libxslt1-dev \
    libzip-dev \
    lsof \
    mailutils \
    msmtp \
    nodejs \
    procps \
    vim \
    zip \
  && rm -rf /var/lib/apt/lists/*

RUN pecl channel-update pecl.php.net && pecl install \
    imagick \
    redis \
    ssh2-1.3.1 \
    xdebug \
  && pecl clear-cache \
  && rm -rf /tmp/pear

RUN docker-php-ext-configure \
    gd --with-freetype --with-jpeg --with-webp \
  && docker-php-ext-install \
    bcmath \
    bz2 \
    calendar \
    exif \
    gd \
    gettext \
    intl \
    mbstring \
    mysqli \
    opcache \
    pcntl \
    pdo_mysql \
    soap \
    sockets \
    sodium \
    sysvmsg \
    sysvsem \
    sysvshm \
    xsl \
    zip \
  && docker-php-ext-enable \
    imagick \
    redis \
    ssh2 \
    xdebug

RUN curl -sS https://getcomposer.org/installer | \
  php -- --install-dir=/usr/local/bin --filename=composer


RUN npm install -g grunt-cli

ENV PHP_MEMORY_LIMIT 2G
ENV PHP_PORT 9000
ENV PHP_PM dynamic
ENV PHP_PM_MAX_CHILDREN 10
ENV PHP_PM_START_SERVERS 4
ENV PHP_PM_MIN_SPARE_SERVERS 2
ENV PHP_PM_MAX_SPARE_SERVERS 6
ENV APP_MAGE_MODE default

COPY conf/www.conf /usr/local/etc/php-fpm.d/
COPY conf/php.ini /usr/local/etc/php/
COPY conf/php-fpm.conf /usr/local/etc/
COPY bin/* /usr/local/bin/

USER app:app
VOLUME /var/www
WORKDIR /var/www

CMD ["/usr/local/bin/start"]
