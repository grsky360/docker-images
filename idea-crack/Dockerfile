FROM curlimages/curl

ENV URL=https://github.com//ilanyu/ReverseProxy/releases/download/v1.4/ReverseProxy_linux_amd64

WORKDIR /app

RUN curl -k -o idea_crack ${URL}
RUN chmod +x idea_crack

FROM alpine

WORKDIR /app

COPY --from=0 /app/idea_crack /app/idea_crack

EXPOSE 8888

CMD [ "/app/idea_crack" ]
