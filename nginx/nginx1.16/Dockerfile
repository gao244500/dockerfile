FROM  centos
MAINTAINER locutus "gao@shuang"
RUN  yum -y install gcc gcc-c++ make libtool gcc gcc-c++ automake autoconf libtool make zlib zlib-devel pcre pcre-devel openssl openssl-devel
WORKDIR  cd /usr/src/
COPY  nginx-1.16.0.tar.gz    /usr/src/
RUN  tar zxf /usr/src/nginx-1.16.0.tar.gz -C /usr/src/ &&cd /usr/src/ &&  mv nginx-1.16.0 nginx
workdir  /usr/src/nginx/
RUN groupadd www   &&  useradd -g www www -s /sbin/nologin
RUN  ./configure --prefix=/usr/local/nginx --with-http_dav_module --with-http_stub_status_module --with-http_addition_module --with-http_sub_module --with-http_flv_module --with-http_mp4_module --with-pcre --with-http_ssl_module --with-http_gzip_static_module --user=www --group=www    && make   -j 4 && make install   &&  ln -s /usr/local/nginx1.10/sbin/* /usr/local/sbin/
run ln -s /usr/local/nginx/sbin/* /usr/local/sbin/
EXPOSE 80
ENTRYPOINT  nginx &&   tail -f /usr/local/nginx/logs/access.log
