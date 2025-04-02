FROM php:8.3-fpm

RUN apt-get update \
    && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libmcrypt-dev \
    autoconf pkg-config libssl-dev zlib1g-dev libicu-dev g++ nginx supervisor \
    && docker-php-ext-install mysqli pdo pdo_mysql gd iconv \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl bcmath \
    && docker-php-ext-install pcntl \
    && pecl install mongodb redis

COPY php.ini /usr/local/etc/php/
RUN docker-php-ext-enable mongodb redis

RUN pecl install excimer


# Configure NGINX
# COPY ./conf.d/* /etc/nginx/conf.d/
# COPY ./certs/*.pem /etc/nginx/ssl/

# Supervisor to manage processes
COPY ./php-fpm.d/www.conf /usr/local/etc/php-fpm.d/www.conf

# Set working directory
WORKDIR /var/www/html

EXPOSE 80 443 8080


# Start Supervisor to manage NGINX and PHP-FPM
CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]