FROM php
LABEL Author="Attiq ur Rehman h.attiqurrehman2@gmail.com"

RUN apt-get update

RUN apt-get install -y apache2

RUN apt-get -y install software-properties-common && \
    add-apt-repository ppa:ondrej/php && \
    apt-get update

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get -y install php7.4 libapache2-mod-php php-mysql php-zip php-mbstring

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

RUN composer global require laravel/installer

RUN apt-get install unzip
RUN apt-get -y install php7.4-xml
RUN apt-get -y install php-mongodb

ENV PATH="~/.composer/vendor/bin:${PATH}"

COPY ./000-default.conf /etc/apache2/sites-available/000-default.conf

RUN a2enmod rewrite

WORKDIR /var/www/html

EXPOSE 80

CMD bash -c "source /etc/apache2/envvars && apache2 -DFOREGROUND"
