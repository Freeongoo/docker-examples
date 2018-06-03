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
RUN apt-get -y install php5.6 php5.6-common php5.6-cli php5.6-mysql php5.6-sqlite libapache2-mod-php5.6 php5.6-fpm php5.6-mcrypt php5.6-mbstring php5.6-curl php5.6-xml php5.6-bcmath php5.6-mail

# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

# Enable apache mods.
RUN a2enmod php5.6
RUN a2enmod rewrite
RUN a2enmod ssl
RUN a2enmod include
RUN a2enmod proxy
RUN a2enmod proxy_http

# copy config php ini
COPY conf/php/php.ini /etc/php/5.6/apache2/conf.d/
COPY conf/php/php.ini /etc/php/5.6/cli/conf.d/

RUN /etc/init.d/apache2 restart

COPY src/ /var/www/html/
WORKDIR /var/www/html
EXPOSE 80
CMD /usr/sbin/apache2ctl -D FOREGROUND