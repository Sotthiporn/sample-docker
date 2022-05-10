# Base Image
FROM php:7.4-apache

# Administrator
USER root

#Internal Environment
ENV RUN_PORT 6060
ENV WORK_DIR /api

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
EXPOSE ${APP_PORT}
