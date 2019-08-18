FROM php:7.2.7-fpm

RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libmcrypt-dev \
    libpng-dev \
    imagemagick \
    libmagick++-dev \
    libmagickwand-dev \
    mysql-client \
    nano \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && docker-php-ext-install \
           pdo \
           pdo_mysql \
           bcmath \
           gd \
           zip \
           intl \
           opcache \
    && pecl install apcu_bc \
    && pecl install imagick  \
    && docker-php-ext-enable apcu \
    && docker-php-ext-enable imagick

RUN touch /usr/local/etc/php/conf.d/custom.ini \
    && echo "memory_limit = 4096M;" >> /usr/local/etc/php/conf.d/custom.ini \
    && echo "realpath_cache_size = 16M;" >> /usr/local/etc/php/conf.d/custom.ini \
    && echo "realpath_cache_ttl = 7200;" >> /usr/local/etc/php/conf.d/custom.ini \
    && echo "upload_max_filesize = 1200M;" >> /usr/local/etc/php/conf.d/custom.ini \
    && echo "post_max_size = 2000M;" >> /usr/local/etc/php/conf.d/custom.ini

RUN touch /usr/local/etc/php/conf.d/opcache.ini \
    && echo "opcache.enable=1;" >> /usr/local/etc/php/conf.d/opcache.ini \
    && echo "opcache.revalidate_freq=0;" >> /usr/local/etc/php/conf.d/opcache.ini \
    && echo "opcache.validate_timestamps=1;" >> /usr/local/etc/php/conf.d/opcache.ini \
    && echo "opcache.max_accelerated_files=300000;" >> /usr/local/etc/php/conf.d/opcache.ini \
    && echo "opcache.memory_consumption=512;" >> /usr/local/etc/php/conf.d/opcache.ini \
    && echo "opcache.max_wasted_percentage=10;" >> /usr/local/etc/php/conf.d/opcache.ini \
    && echo "opcache.interned_strings_buffer=64;" >> /usr/local/etc/php/conf.d/opcache.ini \
    && echo "opcache.fast_shutdown=1;" >> /usr/local/etc/php/conf.d/opcache.ini

RUN touch /usr/local/etc/php/conf.d/apcu.ini \
    && echo "apc.enable=1;" >> /usr/local/etc/php/conf.d/apcu.ini \
    && echo "apc.enable_cli=0;" >> /usr/local/etc/php/conf.d/apcu.ini \
    && echo "apc.shm_size=256M;" >> /usr/local/etc/php/conf.d/apcu.ini \
    && echo "apc.mmap_file_mask=/tmp/apc.XXXXXX;" >> /usr/local/etc/php/conf.d/apcu.ini


WORKDIR /var/www/symfony

RUN chown www-data:www-data /var/www

# only for dev environment
RUN usermod -u 1000 www-data