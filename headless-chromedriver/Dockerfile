FROM alpine:edge

RUN apk add --no-cache dumb-init chromium chromium-chromedriver

EXPOSE 4444

ENTRYPOINT ["/usr/bin/dumb-init", "--"]
CMD ["chromedriver", "--port=4444", "--whitelisted-ips="]
