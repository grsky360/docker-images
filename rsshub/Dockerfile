FROM diygod/rsshub:latest

WORKDIR /app-doc

ENV GIT_MASTER_ZIP_URL=https://github.91chifun.workers.dev//https://github.com/DIYgod/RSSHub/archive/master.zip
# ENV GIT_MASTER_ZIP_URL=https://github.com/DIYgod/RSSHub/archive/master.zip

RUN apt-get update && apt-get install -y wget unzip --no-install-recommends && rm -rf /var/lib/apt/lists/* && \
    wget --no-check-certificate ${GIT_MASTER_ZIP_URL} && \
    unzip master.zip && apt purge -y wget unzip && \
    yarn config set strict-ssl false && yarn global add http-server && \
    cd /app-doc/RSSHub-master/docs && \
    yarn init -y && \
    yarn add vuepress pinyin @vuepress/plugin-back-to-top @vuepress/plugin-google-analytics @vuepress/plugin-pwa && \
    npx vuepress build . && \
    rm -rf /app-doc/master.zip && rm -rf /app-doc/RSSHub-master/docs/node_modules
# RUN rm -rf /root/.npm/_cacache

WORKDIR /app

EXPOSE 1200
EXPOSE 1201

CMD ["/bin/sh", "-c", "$(http-server -p 1201 /app-doc/RSSHub-master/docs/.vuepress/dist > http.log 2>&1 &) && cd /app && yarn start"]
