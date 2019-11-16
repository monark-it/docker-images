# go to hell circle ci... 7.3 for the win
FROM php:7.3-fpm

#Install System Packages
RUN  apt-get update && apt install -y unzip zlib1g-dev libicu-dev libsqlite3-dev sqlite3 libpng-dev  libzip-dev wget

#Install PHP Extensions
RUN  docker-php-ext-install pdo_sqlite pdo_mysql zip pcntl intl gd


#Install wkhtmltopdf Package for pdf generation pdftk
# https://github.com/geerlingguy/ansible-role-java/issues/64#issuecomment-393299088
RUN mkdir -p /usr/share/man/man1
RUN  apt install -y wkhtmltopdf pdftk

RUN yes "" |  pecl install apcu && docker-php-ext-enable apcu
RUN docker-php-ext-install opcache

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer && chmod +x /usr/local/bin/composer
# # Add node to sudoers ( without password )
# USER root
# RUN echo 'node ALL=NOPASSWD: ALL' >> /etc/sudoers.d/50-node \
# && echo 'Defaults    env_keep += "DEBIAN_FRONTEND"' >> /etc/sudoers.d/env_keep

RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get install -y nodejs

RUN apt-get install -y gnupg
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install -y yarn
RUN mkdir /var/www/.npm
RUN chown -R 1000:1000 "/var/www/.npm"


RUN usermod -u 1000 www-data
RUN groupmod -g 1000 www-data
USER www-data

EXPOSE 80
EXPOSE 8000
