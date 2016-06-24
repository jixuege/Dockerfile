# This dockerfile uses the centos 7 image
# Nginx Dockerfile
# Version 1.0
# Author: Leon xie

# Pull base images.
FROM centos/template:1.0

# Define author info.
MAINTAINER linux_xd@sina.com

# Add files.
ADD package/pcre-8.36.tar.gz /usr/local/src
ADD package/nginx-1.6.3.tar.gz /usr/local/src

# Define working directory.
WORKDIR /usr/local/src/nginx-1.6.3

# Install Nginx.
RUN \
		yum install -y wget gcc gcc-c++ make openssl-devel && \
		useradd -s /sbin/nologin -M www && \
		./configure --prefix=/usr/local/nginx --user=www --group=www --with-http_ssl_module --with-http_stub_status_module --with-pcre=/usr/local/src/pcre-8.36 && \
		make && \
		make install && \
		echo "daemon off;" >> /usr/local/nginx/conf/nginx.conf

# Define environment variables.
ENV PATH /usr/local/nginx/sbin:$PATH

# Expose ports.
EXPOSE 80

# Define default command.
CMD ["nginx"]
