FROM php:8.2-fpm

# Set working directory
WORKDIR /var/www

# Set xdebug version
ARG XDEBUG_VERSION=3.2.2

# Install system dependencies
RUN apt-get update && apt-get install -y \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

RUN pecl install redis && docker-php-ext-enable redis

# Install xdebug
RUN pecl install xdebug-${XDEBUG_VERSION}
RUN docker-php-ext-enable xdebug

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
