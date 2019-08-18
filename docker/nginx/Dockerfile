FROM debian:jessie

RUN apt-get update \
    && apt-get install -y nginx \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && echo "daemon off;" >> /etc/nginx/nginx.conf

ADD default.conf /etc/nginx/sites-available/default

# only dev environment
RUN usermod -u 1000 www-data

EXPOSE 80

CMD ["nginx"]