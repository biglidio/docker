FROM debian

RUN apt-get update && apt-get install -y apache2 && apt-get clean

ENV APACHE_LOCK_DIR="/var/lock" \
    APACHE_PID_FILE="/var/run/apache2.pid" \
    APACHE_RUN_USER="www-data" \
    APACHE_RUN_GROUP="www-data" \
    APACHE_LOG_DIR="/var/log/apache2"

LABEL Description="Apache Webserver"

VOLUME /var/www/html

EXPOSE 80

ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]