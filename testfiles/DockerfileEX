FROM php:8.0-apache
RUN apt-get update  
RUN docker-php-ext-install pdo pdo_mysql mysqli
RUN apt-get update -y && apt-get upgrade -y 
#RUN docker-php-ext-install pgsql pdo pdo_pgsql pdo_mysql sockets opcache zip xml ldap soap
RUN apt-get install -y python

RUN apt-get update -y && apt-get install -y \
        g++ \
        libicu-dev \
        libpq-dev \
        libzip-dev \
        zip \
        zlib1g-dev \
    && docker-php-ext-install \
        intl \
        opcache \
        pdo_pgsql \
        pgsql 
    #&& docker-php-ext-install pdo_mysql
WORKDIR /var/www/laravel_docker

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY ./services/apache/default.conf /etc/apache2/apache2.conf 


ENV APACHE_DOCUMENT_ROOT /var/www/html/laravel_docker

RUN sed -ri -e 's!/var/www/html/laravel_docker!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf

CMD ["/usr/sbin/apache2", "-DFOREGROUND"]

#RUN chown -R www-data:www-data /var/www/laravel_docker && a2enmod rewrite

