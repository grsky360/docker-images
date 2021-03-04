FROM node:alpine

ENV NODE_ENV production
ENV TZ Asia/Shanghai

ARG USE_CHINA_REGISTRY=1;

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories
RUN apk --no-cache add curl python make g++

WORKDIR /app
RUN wget --no-check-certificate https://github.com/DIYgod/RSSHub/archive/master.zip

RUN if [ "$USE_CHINA_REGISTRY" = 1 ]; then \
  echo 'use yarn mirror'; yarn config set registry https://registry.npm.taobao.org; \
  fi;

RUN yarn config set strict-ssl false
RUN yarn global add http-server

RUN unzip master.zip

WORKDIR /app/RSSHub-master

RUN yarn

WORKDIR /app/RSSHub-master/docs
RUN yarn init -y
RUN yarn add vuepress pinyin @vuepress/plugin-back-to-top @vuepress/plugin-google-analytics @vuepress/plugin-pwa
RUN npx vuepress build .
RUN http-server -p 1201 .vuepress/dist > http.log 2>&1 &

WORKDIR /app/RSSHub-master

EXPOSE 1200
EXPOSE 1201

CMD ["yarn", "start"]
