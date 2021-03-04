FROM node:alpine

ENV NODE_ENV production
ENV TZ Asia/Shanghai

ARG USE_CHINA_REGISTRY=1;
ARG PUPPETEER_SKIP_CHROMIUM_DOWNLOAD=1;

RUN apk --no-cache add curl python make g++ dumb-init

WORKDIR /app
RUN wget --no-check-certificate https://github.com/DIYgod/RSSHub/archive/master.zip

RUN if [ "$USE_CHINA_REGISTRY" = 1 ]; then \
  echo 'use yarn mirror'; yarn config set registry https://registry.npm.taobao.org; \
  fi;

RUN yarn config set strict-ssl false
# RUN yarn global add http-server vuepress

RUN unzip master.zip

WORKDIR /app/RSSHub-master

RUN yarn
# RUN npx vuepress build docs

# RUN http-server -p 1201 docs/.vuepress/dist

EXPOSE 1200
EXPOSE 1201

ENTRYPOINT ["dumb-init", "--"]
CMD ["yarn", "start"]
