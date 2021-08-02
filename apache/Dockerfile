FROM php:8.0-apache

RUN apt-get upgrade && apt-get update
RUN apt-get install -y vim
RUN apt-get install -y openssl
RUN apt-get install -y libssl-dev
RUN apt-get install -y ssl-cert
RUN apt-get install -y libicu-dev
RUN apt-get install -y unzip
RUN apt-get install -y libxml2
RUN apt-get install -y libxml2-dev
RUN apt-get install -y libonig-dev

RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/*
RUN a2enmod ssl
RUN a2ensite default-ssl
RUN docker-php-ext-install intl
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install simplexml

RUN /bin/bash -c a2enmod rewrite

COPY ./cert/cert-key.pem /usr/local/apache2/cert/
COPY ./cert/cert.pem /usr/local/apache2/cert/

COPY ./conf/httpd.conf /etc/apache2/sites-available/000-default.conf
COPY ./conf/ssl.conf /etc/apache2/sites-available/default-ssl.conf

COPY ./php/php.ini /usr/local/etc/php/php.ini
