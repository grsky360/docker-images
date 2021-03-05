FROM node:alpine

ENV NODE_ENV production
ENV TZ Asia/Shanghai

ENV GIT_MASTER_ZIP_URL=https://github.91chifun.workers.dev//https://github.com/DIYgod/RSSHub/archive/master.zip
# ENV GIT_MASTER_ZIP_URL=https://github.com/DIYgod/RSSHub/archive/master.zip

# RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories
RUN apk --no-cache add python make g++ wget unzip

WORKDIR /app

RUN wget --no-check-certificate ${GIT_MASTER_ZIP_URL}
RUN unzip master.zip

RUN yarn config set registry https://registry.npm.taobao.org
RUN yarn config set strict-ssl false

WORKDIR /app/RSSHub-master

RUN yarn install --production
RUN find node_modules -type f | grep -E "(.idea|.vscode|benchmark.js|.eslintrc.js|changelog|AUTHORS|license|LICENSE|LICENCE|.travis.yml|.eslintrc.json|.eslintrc.yml|Makefile|.npmignore|.DS_Store|.jshintrc|.eslintrc.BSD|.editorconfig|tsconfig.json|.coveralls.yml|appveyor.yml|.gitattributes|.eslintignore|.eslintrc|.eslintignore.BSD|.babelrc|Thumbs.db|Jenkinsfile|Gulpfile|Gruntfile|gulpfile|gruntfile|.tern-project|.stylelintrc|stylelint.config.js|.stylelintrc.json|.stylelintrc.yml|.stylelintrc.yaml|.stylelintrc.js|htmllint.js|.npmrc|.flowconfig|.documentup.json|.yarn-metadata.json|.gitlab-ci.yml|circle.yml|CHANGES|.yarn-integrity|.yarnclean|.yo-rc.json|jest.config.js|karma.conf.js|wallaby.js|wallaby.conf.js|.prettierrc|.prettierrc.yml|.prettierrc.yaml|.prettierrc.toml|.prettierrc.js|.prettierrc.json|prettierrc.config.js|tslint.json)" | xargs rm -rf;
RUN find node_modules -type f | grep -E "\.(md|mdon|markdown|log|ts|swp|jst|coffee|txt|BSD|m?js.map)$" | xargs rm -f;
RUN find node_modules -type d | grep -E "(examples|example|.github|@types)" | xargs rm -rf;

WORKDIR /app/RSSHub-master/docs

RUN yarn init -y
RUN yarn add vuepress pinyin @vuepress/plugin-back-to-top @vuepress/plugin-google-analytics @vuepress/plugin-pwa
RUN npx vuepress build .
RUN mv /app/RSSHub-master/docs/.vuepress/dist /app/docs
RUN rm -rf /app/RSSHub-master/docs

FROM node:alpine

COPY --from=0 /app/RSSHub-master /app
COPY --from=0 /app/docs /app-doc

RUN yarn config set registry https://registry.npm.taobao.org
RUN yarn config set strict-ssl false
RUN yarn global add http-server

EXPOSE 1200
EXPOSE 1201

CMD ["/bin/sh", "-c", "$(http-server -p 1201 /app-doc > /app-doc/http.log 2>&1 &) && cd /app && yarn start"]
