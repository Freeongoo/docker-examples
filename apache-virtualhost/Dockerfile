FROM debian:jessie
RUN apt-get update
RUN apt-get -y install apache2
RUN apt-get -y install vim
RUN apt-get -y install wget

# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

# Enable apache mods.
RUN a2enmod rewrite
RUN a2enmod ssl
RUN a2enmod include
RUN a2enmod proxy
RUN a2enmod proxy_http

# create public dir for virtual host
RUN cd /var/www/ && mkdir mylocal.loc

# copy src to public dir virtual host
COPY src/ /var/www/mylocal.loc/

COPY conf/apache/mylocal.loc.conf /etc/apache2/sites-available/
RUN cd /etc/apache2/sites-available/ && a2ensite mylocal.loc

RUN /etc/init.d/apache2 restart

WORKDIR /var/www/html
EXPOSE 80
CMD /usr/sbin/apache2ctl -D FOREGROUND