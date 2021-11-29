FROM debian:buster-slim

# Preparing the machine to install nginx
RUN apt-get update
RUN apt-get install -y nginx
RUN rm /var/log/nginx/access.log && ln -s /dev/stdout /var/log/nginx/access.log
RUN rm /var/log/nginx/error.log && ln -s /dev/stderr /var/log/nginx/error.log

#COPY ./html/*.html /var/www/html/
#COPY ./html/*.html ./html/assets/ ./html/css/ /var/www/html/
#ADD ./html/ /var/www/html/
#ADD ./html.tar.gz /var/www/
ADD http://example.com/index.html /var/www/html/example.html
CMD ["/usr/sbin/nginx", "-g", "daemon off;"]