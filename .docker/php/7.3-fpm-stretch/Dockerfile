FROM php:7.3-fpm-stretch

ENV DEPS \
    autoconf \
    cmake \
    file \
    g++ \
    gcc \
    libc-dev \
    libpcre3-dev \
    libpcre++-dev \
    make \
    git \
    pkgconf \
    re2c \
    bash \
    nano \
    mc \
    wget \
    # for GD
    libfreetype6-dev \
    libpng-dev  \
    libjpeg62-turbo-dev \
    # for soap
    libxml2-dev \
    # for intl
    gettext \
    # for bz2
    libbz2-dev \
    # for xsl
    libxslt-dev \
    # for mcrypt
    libmcrypt-dev \
    # for ftp
    openssl \
    # for gmp
    libgmp10 libgmp-dev

# copy configs
COPY ./etc/php.ini /usr/local/etc/php/php.ini

RUN set -xe \
    # install deps
    && apt update -qq \
    && DEBIAN_FRONTEND=noninteractive apt install --no-install-recommends -y $DEPS \
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
    && docker-php-ext-configure gmp \
    && docker-php-ext-install -j$(nproc) \
        gd \
        gmp \
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
    && pecl install mcrypt-1.0.2 \
    && docker-php-ext-enable mcrypt \
    # composer
    && curl -sS https://getcomposer.org/installer | php -- \
        --filename=composer \
        --install-dir=/usr/local/bin && \
        echo "alias composer='composer'" >> /root/.bashrc && \
        composer \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/*

COPY docker-php-entrypoint /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-php-entrypoint
ENTRYPOINT ["docker-php-entrypoint"]

CMD ["php-fpm"]
