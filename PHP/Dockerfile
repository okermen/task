FROM php:8.2-apache
ENV DB_CONNECTION=sqlsrv
ENV DB_HOST=localhost
RUN apt-get update
RUN apt-get upgrade
RUN apt-get install -y gnupg
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/config/debian/11/prod.list | tee /etc/apt/sources.list.d/mssql-release.list
RUN apt-get update
RUN ACCEPT_EULA=Y apt-get install -y msodbcsql18
RUN apt-get install -y unixodbc unixodbc-dev && pecl install sqlsrv-5.11.1 pdo_sqlsrv-5.11.1  
RUN echo extension=php_pdo_sqlsrv_82_ts.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
RUN echo extension=php_sqlsrv_82_ts.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
RUN docker-php-ext-enable sqlsrv pdo_sqlsrv
COPY ./QuickDbTest.php /var/www/html/index.php
RUN chmod -R 777 /var/www/html/
EXPOSE 80
CMD ["apache2-foreground"]




