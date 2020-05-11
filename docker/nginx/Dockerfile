FROM centos:7

EXPOSE 80 443

RUN yum update -y && yum install -y epel-release

RUN yum install -y nginx \
                    vim

COPY ./nginx.conf /etc/nginx/conf.d/default.conf

WORKDIR /var/www

CMD ["nginx", "-g", "daemon off;"]
