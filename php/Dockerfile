ARG PHP_VERSION
ARG PHP_IMAGES_SUFFIX=fpm
FROM php:${PHP_VERSION}-${PHP_IMAGES_SUFFIX}
ARG WEBROOT_PATH
RUN mkdir -p ${WEBROOT_PATH} \
    && usermod -u 1000 www-data \
    && docker-php-ext-install pdo_mysql
ARG INSTALL_PHPREDIS_EXTENSION=false
ARG PHPREDIS_VERSION
RUN if [ ${INSTALL_PHPREDIS_EXTENSION} = true ];  then \
    curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/${PHPREDIS_VERSION}.tar.gz \
    && tar xfz /tmp/redis.tar.gz \
    && mkdir -p /usr/src/php/ext \
    && mv phpredis-${PHPREDIS_VERSION} /usr/src/php/ext/redis \
    && docker-php-ext-install redis \
    && rm -rf /usr/src/php \
    && rm -rf /tmp/redis.tar.gz \
;fi
    # && pecl install -o -f redis \
    # && docker-php-ext-enable redis \
    # && rm -rf /tmp/pear \
    # && docker-php-ext-install redis