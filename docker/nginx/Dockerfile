FROM home-php

EXPOSE 80 443

USER root

RUN yum update -y && yum install -y epel-release

RUN yum install -y nginx \
                    vim
COPY ./nginx.conf /etc/nginx/conf.d/default.conf

WORKDIR /var/www
RUN mkdir home \
    && chown www-data:www-data home

CMD ["nginx", "-g", "daemon off;"]
