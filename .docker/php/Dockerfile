FROM php:7.2-fpm-alpine

ENV DEPS \
    autoconf \
    cmake \
    file \
    g++ \
    gcc \
    libc-dev \
    pcre-dev \
    make \
    git \
    pkgconf \
    re2c \
    bash \
    nano \
    # for GD
    freetype-dev \
    libpng-dev  \
    libjpeg-turbo-dev \
    # for soap
    libxml2-dev \
    # for intl
    icu-dev libintl gettext-dev \
    # for bz2
    bzip2-dev \
    # for xsl
    libxslt-dev \
    # for mcrypt
    libmcrypt-dev \
    # for ftp
    openssl-dev

# copy configs
COPY ./etc/php.ini /usr/local/etc/php/php.ini

RUN set -xe \
    # install deps
    && apk update \
    && apk add --no-cache --virtual .build-deps $DEPS \
    # ext
    && docker-php-ext-configure gd \
        --with-gd \
        --with-freetype-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-configure bcmath --enable-bcmath \
    && docker-php-ext-configure intl --enable-intl \
    && docker-php-ext-configure pcntl --enable-pcntl \
    && docker-php-ext-configure mysqli --with-mysqli \
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql \
    && docker-php-ext-configure mbstring --enable-mbstring \
    && docker-php-ext-configure soap --enable-soap \
    && docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-configure ftp --enable-ftp \
    && docker-php-ext-install -j$(nproc) \
        gd \
        bcmath \
        intl \
        pcntl \
        mysqli \
        pdo_mysql \
        soap \
        # bz2 - mkdir: can't create directory '.libs': File exists
        bz2 \
        calendar \
        exif \
        gettext \
        shmop \
        sockets \
        sysvmsg \
        sysvsem \
        sysvshm \
        wddx \
        xsl \
        opcache \
    && pecl install mcrypt-1.0.1 \
    && docker-php-ext-enable mcrypt \
    # composer
    && curl -sS https://getcomposer.org/installer | php -- \
        --filename=composer \
        --install-dir=/usr/local/bin && \
        echo "alias composer='composer'" >> /root/.bashrc && \
        composer \
    # remove cache and tmp files
    && rm -rf /var/cache/apk/* \
    && rm -rf /tmp/*