FROM php:5.6-apache

# Enable Apache modules
RUN a2enmod rewrite headers expires

# Install system dependencies + common PHP extensions
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libwebp-dev \
        libxml2-dev \
        libzip-dev \
        libicu-dev \
        libmcrypt-dev \
        libcurl4-openssl-dev \
        libonig-dev \
        libpq-dev \
        libreadline-dev \
        libxslt1-dev \
        zlib1g-dev \
    && docker-php-ext-configure gd \
        --with-freetype-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
    && docker-php-ext-install -j"$(nproc)" \
        bcmath \
        calendar \
        exif \
        gd \
        gettext \
        intl \
        mbstring \
        mysqli \
        opcache \
        pdo \
        pdo_mysql \
        pdo_pgsql \
        pgsql \
        soap \
        sockets \
        sysvmsg \
        sysvsem \
        sysvshm \
        xml \
        xsl \
        zip \
    && rm -rf /var/lib/apt/lists/*

# Allow .htaccess files to override Apache configuration
RUN sed -i \
    's/AllowOverride None/AllowOverride All/g' \
    /etc/apache2/apache2.conf

# Avoid Apache ServerName warning
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

WORKDIR /var/www/html

EXPOSE 80

CMD ["apache2-foreground"]
