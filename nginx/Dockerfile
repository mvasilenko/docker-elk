FROM ubuntu:xenial
ENV DEBIAN_FRONTEND noninteractive

# Install nginx
RUN groupadd nginx && useradd -g nginx -d /usr/share/nginx/html nginx && \ 
    apt-get update && apt-get install -q -y nginx wget vim curl

# Create self-signed certificate
#RUN openssl req -x509 -batch -nodes -newkey rsa:2048 -keyout /etc/ssl/private/kibana.key -out /etc/ssl/private/kibana.crt -subj /CN=kibana
#RUN chmod 600 /etc/ssl/private/kibana.key

# Add configurations and htpasswd
ADD conf/nginx.conf /etc/nginx/nginx.conf
ADD conf/kibana.conf /etc/nginx/sites-available/kibana.conf
ADD conf/kibana.crt /etc/ssl/private/kibana.crt
ADD conf/kibana.key /etc/ssl/private/kibana.key
ADD conf/htpasswd /etc/nginx/htpasswd
RUN ln -s /etc/nginx/sites-available/kibana.conf /etc/nginx/sites-enabled/10-kibana.conf && \
    ln -sf /dev/stdout /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 8443
EXPOSE 9200
CMD ["nginx", "-g", "daemon off;"]

