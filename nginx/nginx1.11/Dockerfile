FROM  centos
MAINTAINER locutus "gao@shuang"
RUN  yum -y install gcc gcc-c++ make libtool gcc gcc-c++ automake autoconf libtool make zlib zlib-devel pcre pcre-devel openssl openssl-devel
WORKDIR  cd /usr/src/
COPY  nginx-1.11.3.tar.gz    /usr/src/
RUN  tar zxf /usr/src/nginx-1.11.3.tar.gz -C /usr/src/ &&cd /usr/src/ &&  mv nginx-1.11.3 nginx
RUN cd /usr/src/nginx/src  && sed '13d ' /usr/src/nginx/src/core/nginx.h -i && sed '13d ' /usr/src/nginx/src/core/nginx.h -i && sed '12a #define NGINX_VERSION      "100"' /usr/src/nginx/src/core/nginx.h -i && sed '13a #define NGINX_VER          "gao/" NGINX_VERSION' /usr/src/nginx/src/core/nginx.h -i  && sed '49d' /usr/src/nginx/src/http/ngx_http_header_filter_module.c  -i && sed '48a static char ngx_http_server_string[] = "Server: gao" CRLF;' /usr/src/nginx/src/http/ngx_http_header_filter_module.c  -i && sed '29d' /usr/src/nginx/src/http/ngx_http_special_response.c  -i && sed '28a "<hr><center>gao</center>" CRLF' /usr/src/nginx/src/http/ngx_http_special_response.c -i
workdir  /usr/src/nginx/
RUN groupadd www   &&  useradd -g www www -s /sbin/nologin
RUN  ./configure --prefix=/usr/local/nginx --with-http_dav_module --with-http_stub_status_module --with-http_addition_module --with-http_sub_module --with-http_flv_module --with-http_mp4_module --with-pcre --with-http_ssl_module --with-http_gzip_static_module --user=www --group=www    && make   -j 4 && make install   &&  ln -s /usr/local/nginx1.10/sbin/* /usr/local/sbin/
run ln -s /usr/local/nginx/sbin/* /usr/local/sbin/
EXPOSE 80
ENTRYPOINT  nginx &&   tail -f /usr/local/nginx/logs/access.log
