FROM php:7.4-fpm

copy apt.sources.list /etc/apt/sources.list

RUN apt-get update 

# gd扩展
RUN apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        zlib1g-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd

# # 添加Kafka扩展
# RUN apt-get install -y librdkafka-dev
# RUN pecl install rdkafka
# RUN docker-php-ext-enable rdkafka

# redis扩展
RUN pecl install redis-5.1.1
RUN docker-php-ext-enable redis

# xlswriter扩展
RUN pecl install xlswriter
RUN docker-php-ext-enable xlswriter

# xdebug扩展
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

# 安装自带扩展
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install zip

RUN apt autoremove -y

RUN cp "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

RUN curl -o /usr/local/bin/composer https://mirrors.aliyun.com/composer/composer.phar && chmod +x /usr/local/bin/composer
RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

# 通过entrypoint 修改挂载目录权限为www-data
# 容器内 www-data 和 宿主机 UID不一致，无法两边同时编辑
# COPY docker-php-entrypoint /usr/local/bin/

# 修改www-data用户的 UID GID 和 宿主机用户一致
RUN groupmod -g 1000 www-data && usermod -u 1000 -g 1000 www-data
