FROM php:7.2.0-apache

ARG PROJECT

ENV APACHE_DOCUMENT_ROOT /var/www/$PROJECT/public

RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf


# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# Install package
RUN apt-get update && apt-get install -y \
  vim \
  git \
  subversion \
  zlib1g-dev

RUN apt-get -y update \
    && apt-get install -y libicu-dev\  
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl

# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-install pdo pdo_mysql zip

# Workaround for write permission on write to MacOS X volumes
# See https://github.com/boot2docker/boot2docker/pull/534
RUN usermod -u 1000 www-data

# Enable Apache mod_rewrite
RUN a2enmod rewrite


#ALIASES
RUN echo 'alias sf="php app/console"' >> ~/.bashrc
RUN echo "alias ll='ls -l'" >> ~/.bashrc

COPY ./docker/webserver/apache/apache_default /etc/apache2/sites-available/000-default.conf

WORKDIR /var/www/$PROJECT

#INFORMATION
#zlib1g-dev compression library - development
#libicu-dev: Development files for International Components for Unicode (ICU)
#intl: Internationalization extension (further is referred as Intl) is a wrapper for » ICU library (required by symfony framework)

