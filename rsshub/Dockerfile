FROM diygod/rsshub:latest

WORKDIR /app-doc

RUN apt-get update && apt-get install -y wget unzip --no-install-recommends && rm -rf /var/lib/apt/lists/*

RUN wget --no-check-certificate https://github.91chifun.workers.dev//https://github.com/DIYgod/RSSHub/archive/master.zip
# RUN wget --no-check-certificate https://github.com/DIYgod/RSSHub/archive/master.zip

RUN unzip master.zip

RUN yarn config set strict-ssl false
RUN yarn global add http-server

WORKDIR /app-doc/RSSHub-master/docs

RUN yarn init -y
RUN yarn add vuepress pinyin @vuepress/plugin-back-to-top @vuepress/plugin-google-analytics @vuepress/plugin-pwa
RUN npx vuepress build .

RUN rm -rf /app-doc/master.zip
RUN rm -rf /app-doc/RSSHub-master/docs/node_modules
RUN rm -rf /root/.npm/_cacache

WORKDIR /app

EXPOSE 1200
EXPOSE 1201

CMD ["/bin/sh", "-c", "$(http-server -p 1201 /app-doc/RSSHub-master/docs/.vuepress/dist > http.log 2>&1 &) && cd /app && yarn start"]
