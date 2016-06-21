FROM php:5.6-apache
RUN usermod -u 1000 www-data
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \ 
        libxml2-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt soap mbstring pdo_mysql \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd 
ADD ./apache/default.conf /etc/apache2/sites-available/default.conf
RUN a2enmod rewrite && a2ensite default 
CMD ["apache2-foreground"]
