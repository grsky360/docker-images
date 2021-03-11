FROM node:alpine

# RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories
RUN apk --no-cache add subversion python3 make g++ wget unzip

WORKDIR /app

RUN svn checkout --non-interactive --trust-server-cert-failures=unknown-ca,cn-mismatch,expired,not-yet-valid,other https://github.com/DIYgod/RSSHub/trunk/docs

WORKDIR /app/docs

RUN yarn config set registry https://registry.npm.taobao.org
RUN yarn config set strict-ssl false

RUN yarn init -y
RUN yarn add vuepress pinyin @vuepress/plugin-back-to-top @vuepress/plugin-google-analytics @vuepress/plugin-pwa
RUN npx vuepress build .
RUN mv /app/docs/.vuepress/dist /app/dist

FROM busybox

ENV DEPLOYMENT_PATH=/deployment

COPY --from=0 /app/dist /app

VOLUME [ "${DEPLOYMENT_PATH}" ]

CMD [ "/bin/sh", "-c", "mkdir -p ${DEPLOYMENT_PATH} && rm -rf ${DEPLOYMENT_PATH}/* && cp -R /app/* ${DEPLOYMENT_PATH}" ]
