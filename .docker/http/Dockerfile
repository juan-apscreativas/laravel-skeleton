FROM php:8.2.7-apache-bullseye
COPY --from=composer:2.4.3 /usr/bin/composer /usr/bin/composer

# system dependencies
RUN apt-get update \
    && apt-get install -qq --yes --no-install-recommends \
    apt-utils \
    ca-certificates \
    libxml2-dev \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libxpm-dev \
    libwebp-dev \
    libzip-dev \
    libcurl4-openssl-dev \
    file \
    g++ \
    make \
    uuid-runtime \
    git \
    zip \
    unzip \
    && apt-get autoremove \
    && apt-get clean \
    && apt-get autoclean

# php extensions
RUN docker-php-ext-install -j$(nproc) \
    gd \
    pdo_mysql \
    opcache \
    zip

# enable apache modules and
# test apache configuration
RUN a2enmod rewrite &&\
    apache2ctl configtest

# expose http and https ports
EXPOSE 80

# command
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
