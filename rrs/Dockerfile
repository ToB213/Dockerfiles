# イメージはOpenJDKが17で，Debianは古すぎず安定してそうなのを選んだ
# 最新の安定版およびコードネームについては 
# https://www.debian.org/releases/index.ja.html 
# を確認
FROM openjdk:17-jdk-buster

WORKDIR /app

RUN apt-get update && \
    apt install -y git

RUN git clone https://github.com/roborescue/rcrs-server.git

WORKDIR /app/rcrs-server
