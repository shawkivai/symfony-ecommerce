# Use a PHP-FPM image as a base
FROM php:8.2-fpm-alpine

# Install required packages
RUN apk add --no-cache \
    git \
    curl \
    libzip-dev \
    zlib-dev \
    && docker-php-ext-install zip

# Install composer globally
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/

# Create the application directory
WORKDIR /app

# Copy composer.json and composer.lock
COPY composer.json composer.lock ./

# Install dependencies
RUN composer install --no-interaction --optimize-autoloader

# Copy the rest of the application
COPY . .

# Set environment variables
ENV APP_ENV=dev
ENV APP_DEBUG=1

# Expose port 80
EXPOSE 80

# Set working directory
WORKDIR /app/public

# Start the PHP-FPM process
CMD ["php-fpm", "-F"]
