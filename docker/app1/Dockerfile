# this is Dockerfile
FROM ubuntu:22.04
RUN apt-get update -y
RUN apt-get install -y nginx net-tools


RUN sed -i -e 's/listen 80/listen 8080/' /etc/nginx/sites-available/default
RUN sed -i -e '/listen \[::\]:80/d' /etc/nginx/sites-available/default
EXPOSE 8080

COPY index.html  /var/www/html/
COPY docker-entrypoint.sh /
RUN chmod 755 /docker-entrypoint.sh

ENTRYPOINT [ "/docker-entrypoint.sh" ]
# eof


