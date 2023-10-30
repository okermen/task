FROM php:8.2-apache
ENV DB_CONNECTION=sqlsrv
ENV DB_HOST=localhost
ENV ACCEPT_EULA=Y
RUN apt-get update \
    && apt-get install -y gnupg2 libpng-dev libzip-dev \
    && rm -rf /var/lib/apt/lists/*
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
    && curl https://packages.microsoft.com/config/debian/11/prod.list > /etc/apt/sources.list.d/mssql-release.list \
    && echo "Package: unixodbc\nPin: origin \"packages.microsoft.com\"\nPin-Priority: 100\n" >> /etc/apt/preferences.d/microsoft \
    && echo "Package: unixodbc-dev\nPin: origin \"packages.microsoft.com\"\nPin-Priority: 100\n" >> /etc/apt/preferences.d/microsoft \
    && echo "Package: libodbc1:amd64\nPin: origin \"packages.microsoft.com\"\nPin-Priority: 100\n" >> /etc/apt/preferences.d/microsoft \
    && echo "Package: odbcinst\nPin: origin \"packages.microsoft.com\"\nPin-Priority: 100\n" >> /etc/apt/preferences.d/microsoft \
    && echo "Package: odbcinst1debian2:amd64\nPin: origin \"packages.microsoft.com\"\nPin-Priority: 100\n" >> /etc/apt/preferences.d/microsoft \
    && apt-get update \
    && apt-get install -y msodbcsql18 mssql-tools18 unixodbc-dev \
    && rm -rf /var/lib/apt/lists/*
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/install-php-extensions
RUN chmod uga+x /usr/bin/install-php-extensions \
    && install-php-extensions pdo_sqlsrv sqlsrv 
COPY ./QuickDbTest.php /var/www/html/index.php
RUN chmod -R 777 /var/www/html/
EXPOSE 80
CMD ["apache2-foreground"]




