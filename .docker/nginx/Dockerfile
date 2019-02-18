FROM nginx:1.15.3-alpine

#RUN set -xe \
#    # install deps
#    && apk update \
#    && apk add --no-cache --virtual .build-deps bash nano

COPY ./etc/fastcgi_params /etc/nginx/fastcgi_params
COPY ./etc/nginx.conf /etc/nginx/nginx.conf

