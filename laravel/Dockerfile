# Base Image
FROM php:7.4-apache

#Adminstrator
USER root

#Internal Environment
ENV RUN_PORT 6060
ENV WORK_DIR /api


# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    libzip-dev \
    unzip \
    git \
    libonig-dev \
    curl

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*


#Install php extension & mysql driver
RUN docker-php-ext-install pdo pdo_mysql sockets


#Download composer
RUN curl -sS https://getcomposer.org/installer | php -- \
    --install-dir=/usr/local/bin --filename=composer


# Working Directory
WORKDIR ${WORK_DIR}

# Copy Current Directory to Contatiner Directory
COPY . .

# Run When Build Image
RUN composer install


# Run When Build Container
CMD php artisan key:generate && \
    php artisan migrate --seed && \
    php artisan serve --host 0.0.0.0 --port=${RUN_PORT}


# Expose Port
EXPOSE ${RUN_PORT}
