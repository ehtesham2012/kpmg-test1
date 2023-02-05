# Use an official Ubuntu image as the base image
FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive
# Install necessary packages
RUN apt-get update && apt-get install -y \
    apache2 \
    php-mbstring \
    php-xml \
    php-intl \
    mariadb-server \
    php \
    libapache2-mod-php \
    php-mysql \
    wget

# Download MediaWiki 1.39.1
RUN wget https://releases.wikimedia.org/mediawiki/1.39/mediawiki-1.39.1.tar.gz
RUN tar -xzf mediawiki-1.39.1.tar.gz
RUN rm mediawiki-1.39.1.tar.gz
RUN mv mediawiki-1.39.1 /var/www/html/mediawiki

# Configure Apache to use MediaWiki
RUN rm /var/www/html/index.html
RUN echo "<VirtualHost *:80>\n\
    ServerAdmin webmaster@localhost\n\
    DocumentRoot /var/www/html/mediawiki\n\
    ErrorLog ${APACHE_LOG_DIR}/error.log\n\
    CustomLog ${APACHE_LOG_DIR}/access.log combined\n\
</VirtualHost>" > /etc/apache2/sites-available/000-default.conf

# Copy the LocalSettings.php file to the MediaWiki installation directory
COPY LocalSettings.php /var/www/html/mediawiki/
COPY LocalSettings.php /var/www/html/mediawiki/mw-config/

# Expose port 80
EXPOSE 80

# Start Apache
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
