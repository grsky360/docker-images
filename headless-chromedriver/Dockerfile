FROM alpine:edge

RUN apk add dumb-init chromium chromium-chromedriver fontconfig
RUN apk add wqy-zenhei --update-cache --repository http://nl.alpinelinux.org/alpine/edge/testing --allow-untrusted
RUN rm -rf /var/cache/apk/*

EXPOSE 4444

ENTRYPOINT ["/usr/bin/dumb-init", "--"]
CMD ["chromedriver", "--port=4444", "--whitelisted-ips="]
