FROM php:7.4-apache

RUN apt-get update && apt-get install -y unixodbc unixodbc-dev && pecl install sqlsrv pdo_sqlsrv && docker-php-ext-enable sqlsrv pdo_sqlsrv

COPY ./QuickDbTest.php /var/www/html
EXPOSE 80

WORKDIR  /var/www/
CMD ["apache2-foreground"]

