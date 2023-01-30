FROM php:7.4-apache
#MAINTAINER docker-web

RUN apt-get update \
  && apt-get install -y zlib1g-dev libpq-dev mariadb-client unzip libzip-dev git \
  && docker-php-ext-install zip pdo_mysql mysqli \
  && docker-php-ext-enable mysqli
RUN apt -y install sudo
RUN useradd -s /bin/bash -G sudo -m ec2-user
RUN echo "ec2-user:password" | chpasswd
RUN echo "root:root" | chpasswd

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === '55ce33d7678c5a611085589f1f3ddf8b3c52d662cd01d4ba75c0ee0459970c2200a51f492d557530c71c15d8dba01eae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN sudo mv composer.phar /usr/local/bin/composer

RUN ln -s /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/rewrite.load
RUN ln -s /etc/apache2/mods-available/vhost_alias.load /etc/apache2/mods-enabled
RUN echo ServerName $HOSTNAME:80 > /etc/apache2/conf-available/fqdn.conf && a2enconf fqdn

COPY ./vhost.conf /etc/apache2/sites-available/vhost.conf
RUN a2ensite vhost.conf

COPY ./php.ini /usr/local/etc/php/

#WORKDIR /var/www/html
USER ec2-user
WORKDIR /home/ec2-user/environment