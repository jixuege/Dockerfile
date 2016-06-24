# This dockerfile uses the centos 7 image
# Nginx Dockerfile
# Version 1.0
# Author: jixuege

# Pull base images.
FROM centos

# Define author info.
MAINTAINER  jixuege  linux_xiedi@sian.com

# To optimize the system ,if you don't need ,just skip this step.
#Commands
RUN \
        > /etc/locale.conf && echo "LANG=zh_CN.UTF-8"> /etc/locale.conf && source /etc/locale.conf &&  \	
	yum -y update; yum clean all && \
	yum -y install wget  && \
	mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak && \
        wget -O /etc/yum.repos.d/CentOS-Base.repo  http://mirrors.aliyun.com/repo/Centos-7.repo && \
        wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo && \
        yum -y install kde-l10n-Chinese glibc-common git vim tree lsof net-tools supervisor openssh-server passwd sshpass unzip salt-minion openssh-clients && \
	yum -y reinstall glibc-common &&  \
	echo "root:90docker@jixuege"|chpasswd && echo " export LANG=zh_CN.UTF-8" >>/root/.bashrc &&  \
	useradd test &&  echo "test:justfortest"|chpasswd  &&  \
	mkdir /var/run/sshd && \
	ssh-keygen -q -t rsa -b 2048 -f /etc/ssh/ssh_host_rsa_key -N '' && \
	ssh-keygen -q -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key -N '' && \
	ssh-keygen -q -t ecdsa -f /etc/ssh/ssh_host_ed25519_key -N '' && \
  	\cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime 

# Add files.
ADD  package/nginx-1.10.1.tar.gz /usr/local/src 
ADD conf/supervisord.conf /etc/supervisord.conf

# Define working directory.
WORKDIR /usr/local/src/nginx-1.10.1


# Install Nginx.
RUN \
	yum install -y  gcc  glibc gcc-c++ pcre-devel make openssl-devel && \
	useradd -s /sbin/nologin -M www && \
	./configure --prefix=/usr/local/nginx-1.10.1 --user=www --group=www --with-http_ssl_module  --with-http_gzip_static_module --with-http_stub_status_module && \
	make && \
	make install && \
	ln -s /usr/local/nginx-1.10.1/ /usr/local/nginx

# Env.
ENV LANG zh_CN.UTF-8
ENV LC_ALL zh_CN.UTF-8

# Define default port.
EXPOSE 22 80

#Define default command.
CMD ["supervisord","-n"]
	

