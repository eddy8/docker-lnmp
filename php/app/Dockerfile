ARG PHP_VERSION=7.4
FROM php:${PHP_VERSION}-cli-alpine

ENV TZ=Asia/Shanghai

# init
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories

# Install dev dependencies
RUN apk add --no-cache --virtual .build-deps \
    $PHPIZE_DEPS \
    curl-dev \
    libtool \
    libxml2-dev

# Install production dependencies
RUN apk add --no-cache \
    bash \
    curl \
    freetype-dev \
    g++ \
    gcc \
    git \
    icu-dev \
    icu-libs \
    libc-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libzip-dev \
    make \
    mysql-client \
    openssh-client \
    rsync \
    zlib-dev

# Configure php extensions
RUN docker-php-ext-configure gd --with-freetype --with-jpeg

# Install php extensions
RUN docker-php-ext-install \
    bcmath \
    calendar \
    exif \
    gd \
    intl \
    pdo_mysql \
    pcntl \
    xml \
    zip

# PHP REDIS EXTENSION
ARG INSTALL_PHPREDIS=true

RUN if [ ${INSTALL_PHPREDIS} = true ]; then \
    # Install Php Redis Extension
    if [ $(php -r "echo PHP_MAJOR_VERSION;") = "5" ]; then \
      pecl install -o -f redis-4.3.0; \
    else \
      pecl install -o -f redis; \
    fi \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable redis \
;fi

# Install composer
ENV COMPOSER_HOME /composer
ENV PATH ./vendor/bin:/composer/vendor/bin:$PATH
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer

# Cleanup dev dependencies
RUN apk del -f .build-deps

# 应用自定义脚本 初始化？拉取代码？安装其它相关应用？
# CMD php -S 127.0.0.1:8080