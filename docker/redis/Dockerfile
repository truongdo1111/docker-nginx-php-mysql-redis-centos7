FROM centos/redis-32-centos7

# redis.conf:109 のログファイル設定を有効化したときに必要
USER root
RUN mkdir -p /var/log/redis
RUN chmod -R 777 /var/log/redis
COPY redis.conf /etc/redis/redis.conf
