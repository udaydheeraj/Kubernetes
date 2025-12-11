FROM httpd:2.4

RUN apt-get update && \
    apt-get install -y php php-cli php-mysql && \
    apt-get clean

COPY index.php /usr/local/apache2/htdocs/index.php

EXPOSE 80

CMD ["httpd-foreground"]
