FROM nginx:mainline-alpine

COPY ./conf/nginx_conf.conf /etc/nginx/conf.d/default.conf

CMD ["nginx", "-g", "daemon off;"]