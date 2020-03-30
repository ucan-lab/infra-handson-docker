FROM php:7.4-apache-buster

ENV DB_HOST=shop_db
ENV DB_NAME=shop
ENV DB_USER=phper
ENV DB_PASS=secret

RUN apt-get update
RUN docker-php-ext-install pdo_mysql
