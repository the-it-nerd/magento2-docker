FROM nginx

COPY conf/nginx.conf /etc/nginx/conf.d/default.conf
COPY conf/magento.crt /etc/nginx/ssl/
COPY conf/magento.key /etc/nginx/ssl/

EXPOSE 8080
ENTRYPOINT nginx -g 'daemon off;'
