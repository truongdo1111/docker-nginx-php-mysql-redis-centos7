FROM centos:7

# Install Apache
RUN yum -y update
RUN yum install -y vim \
                   htop \
                   wget

RUN wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
    && wget http://rpms.remirepo.net/enterprise/remi-release-7.rpm \
    && rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm \
    && yum --enablerepo=remi update remi-release

RUN yum --enablerepo=remi-php73 install -y php-fpm php73-php php73-php-pear php73-php-bcmath php73-php-pecl-jsond-devel \
                     php73-php-mysqlnd php73-php-gd php73-php-common php73-php-intl php73-php-cli \
                     php73-php php73-php-xml php73-php-opcache php73-php-pecl-apcu php73-php-pecl-jsond php73-php-pdo \
                     php73-php-gmp php73-php-process php73-php-pecl-imagick php73-php-devel php73-php-soap \
                     php73-php-mcrypt php-mcrypt php-soap php73-php-mbstring \
                     php-redis redis php73-php-redis php71-php-zip

RUN rm -f /usr/bin/php \
    && ln -s /usr/bin/php73 /usr/bin/php

#RUN rm /etc/php-fpm.d/www.conf
ADD ./php-fpm/web.conf /etc/php-fpm.d/web.conf
COPY ./php/php.ini /etc/php/conf.d/php.ini
COPY ./php/dev.ini /etc/php/conf.d/dev.ini

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
ENV PATH $PATH:/root/.composer/vendor/bin

USER root
RUN adduser www-data \
   && mkdir /var/run/php-fpm \
   && chown www-data:www-data /run/php-fpm \
   && chown www-data:www-data /var/log/php-fpm/ \
   && chown www-data:www-data /usr/bin/

USER www-data
EXPOSE 9000

CMD ["php-fpm", "-F"]
