# ubuntu 20.04 with Apache2 and PHP 7.4
FROM ubuntu:20.04


# set environment variables for the installation of the Apache2 to avoid questions
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Europe/Berlin

# install apache2 and PHP 7.4 and the PHP module for MySQL
RUN apt-get update && \
    apt-get install -y \
    apache2 \
    php7.4 \
    libapache2-mod-php7.4 \
    php7.4-mysql && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# aktivate PHP module in Apache and set index.php as default file
RUN echo "LoadModule php7_module /usr/lib/apache2/modules/libphp7.4.so" > /etc/apache2/mods-available/php7.load && \
    echo "<FilesMatch \.php$>" > /etc/apache2/mods-available/php7.conf && \
    echo "    SetHandler application/x-httpd-php" >> /etc/apache2/mods-available/php7.conf && \
    echo "</FilesMatch>" >> /etc/apache2/mods-available/php7.conf && \
    echo "DirectoryIndex index.php index.html" >> /etc/apache2/mods-available/php7.conf && \
    a2enmod php7.4

# copy the content of the src directory to the web root
#COPY ./src /var/www/html/

# expose port 80
EXPOSE 80

# Start Apache in foreground mode
CMD ["apachectl", "-D", "FOREGROUND"]
