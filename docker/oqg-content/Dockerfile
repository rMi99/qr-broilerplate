FROM php:8.1-fpm

# Install system dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    curl \
    pkg-config \
    libonig-dev \
    libzip-dev

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql mysqli mbstring exif pcntl bcmath gd zip

# Configure and install GD extension with support for JPEG and FreeType
RUN docker-php-ext-configure gd --with-freetype --with-jpeg && \
    docker-php-ext-install -j$(nproc) gd

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/html

COPY ./src/oqg-email .

# Install PHP dependencies
RUN composer install --ignore-platform-req=ext-zip

# Set permissions for storage and cache directories
RUN chown -R www-data:www-data storage bootstrap/cache && \
    chmod -R 775 storage bootstrap/cache

# Artisan commands
RUN php artisan package:discover --ansi && \
    php artisan key:generate && \
    php artisan cache:clear && \
    php artisan config:clear && \
    php artisan route:clear

# Expose port 8001
EXPOSE 8002

CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8002"]
