# イメージはOpenJDKが17で，Debianは古すぎず安定してそうなのを選んだ
# 最新の安定版およびコードネームについては
# https://www.debian.org/releases/index.ja.html
# を確認
FROM openjdk:17-jdk-buster

WORKDIR /app

RUN apt-get update && \
    apt install -y git curl

RUN git clone https://github.com/roborescue/rcrs-server.git

WORKDIR /app/rcrs-server

# Python 3.12をインストール
RUN apt-get update && \
    apt-get install -y python3

RUN cd ~ 

RUN apt update && \
    apt install -y build-essential libssl-dev zlib1g-dev \
    libbz2-dev libreadline-dev libsqlite3-dev curl \
    libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev

RUN wget https://www.python.org/ftp/python/3.12.0/Python-3.12.0.tgz && \
    tar -xzvf Python-3.12.0.tgz 

RUN cd Python-3.12.0 && \
    ./configure && \
    make && \
    make install

RUN whereis python3.12 && \
    update-alternatives --install /usr/bin/python python /usr/local/bin/python3.12 1 && \
    update-alternatives --install /usr/bin/python3 python3 /usr/local/bin/python3.12 1

RUN  curl -sSL https://install.python-poetry.org | python3.12 -

# Poetryのパスを通す
RUN echo 'export PATH="/root/.local/bin:$PATH"' >> ~/.bashrc && \
    . ~/.bashrc

# Poetryのバージョンを確認
RUN poetry --version

# pip
RUN curl -kL https://bootstrap.pypa.io/get-pip.py | python
