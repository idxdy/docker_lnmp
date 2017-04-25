FROM nginx:1.11

ADD  nginx.conf      /etc/nginx/nginx.conf
ADD  sites-enabled/*    /etc/nginx/conf.d/
RUN  mkdir /opt/htdocs && mkdir /opt/logs && mkdir /opt/logs/nginx
RUN  chown -R www-data.www-data /opt/htdocs /opt/logs /opt/conf/nginx.vhost

VOLUME ["/opt"]