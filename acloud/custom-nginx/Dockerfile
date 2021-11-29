# Simple nginx image
# FROM scratch allows you to build a blank image
FROM ubuntu:bionic

ENV NGINX_VERSION 1.14.0

RUN apt-get update && apt-get install -y curl
RUN apt-get update && apt-get install -y nginx


WORKDIR /var/www/html
#WORKDIR /var
#WORKDIR www
#WORKDIR html

#COPY index.html ./
ADD index.html ./

EXPOSE 80

CMD [ "nginx", "-g", "daemon off;" ]

STOPSIGNAL SIGTERM
HEALTHCHECK CMD curl localhost:80

