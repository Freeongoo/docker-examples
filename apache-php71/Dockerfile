FROM debian:jessie
RUN apt-get update
RUN apt-get -y install vim
RUN apt-get -y install wget

# add rep for php
RUN apt-get -y install apt-transport-https ca-certificates
RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN echo "deb https://packages.sury.org/php/ jessie main" > /etc/apt/sources.list.d/php.list
RUN apt-get -y update

# install php
RUN apt-get -y install php7.1 php7.1-common php7.1-cli php7.1-mysql php7.1-sqlite libapache2-mod-php7.1 php7.1-fpm php7.1-mcrypt php7.1-mbstring php7.1-curl php7.1-xml php7.1-bcmath php7.1-mail

# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

# Enable apache mods.
RUN a2enmod php7.1
RUN a2enmod rewrite
RUN a2enmod ssl
RUN a2enmod include
RUN a2enmod proxy
RUN a2enmod proxy_http

# copy config php ini
COPY conf/php/php.ini /etc/php/7.1/apache2/conf.d/
COPY conf/php/php.ini /etc/php/7.1/cli/conf.d/

RUN /etc/init.d/apache2 restart

COPY src/ /var/www/html/
WORKDIR /var/www/html
EXPOSE 80
CMD /usr/sbin/apache2ctl -D FOREGROUND