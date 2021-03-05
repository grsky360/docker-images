FROM nginx:alpine

COPY default.conf /etc/nginx/conf.d/default.conf

WORKDIR /html

VOLUME [ "/html", "/etc/nginx/conf.d" ]

EXPOSE 80
