FROM php:8.2-apache
RUN apt-get update && apt-get install -y unixodbc unixodbc-dev && pecl install sqlsrv pdo_sqlsrv && docker-php-ext-enable sqlsrv pdo_sqlsrv
COPY ./QuickDbTest.php /var/www/html/QuickDbTest.php
EXPOSE 80
CMD ["apache2-foreground"]


