FROM php:8.1-fpm

# Instalar dependências
RUN apt-get update && apt-get install -y \
    libzip-dev \
    zip \
    libonig-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* 

# Instalar oniguruma manualmente
RUN cd /tmp && \
    curl -LO https://github.com/kkos/oniguruma/releases/download/v6.9.7.1/onig-6.9.7.1.tar.gz && \
    tar -zxvf onig-6.9.7.1.tar.gz && \
    cd onig-6.9.7.1 && \
    ./configure && \
    make && \
    make install

# Instalar extensões PHP
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl

# Configurar PHP
COPY ./docker/php-fpm/php.ini /usr/local/etc/php/php.ini

WORKDIR /var/www/html

CMD ["php-fpm"]
