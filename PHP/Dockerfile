FROM php:8.2-apache
RUN apt-get update && apt-get install -y unixodbc unixodbc-dev && pecl install sqlsrv-5.11.1 pdo_sqlsrv-5.11.1  
RUN echo extension=php_pdo_sqlsrv_82_ts.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/10_pdo_sqlsrv.ini
RUN echo extension=php_sqlsrv_82_ts.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20_sqlsrv.ini
RUN docker-php-ext-enable sqlsrv pdo_sqlsrv
COPY ./QuickDbTest.php /var/www/html/index.php
RUN chmod -R 777 /var/www/html/
EXPOSE 80
CMD ["apache2-foreground"]


