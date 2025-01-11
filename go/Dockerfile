FROM ubuntu:latest

RUN apt-get update -y \
    && apt-get install -y \
    software-properties-common \ 
    curl \
    git \
    neovim \
    nodejs \
    npm \
    python3-pip \
    python3 \
    && apt-get clean \ 
    && rm -rf /var/lib/apt/lists/* 

RUN add-apt-repository ppa:longsleep/golang-backports -y \ 
    && apt-get update -y \
    && apt-get install -y golang-go \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

ENV GOPATH=/root/go
ENV PATH=$PATH:/usr/local/go/bin:$GOPATH/bin

RUN mkdir -p /root/.config/nvim/ \
    && mkdir -p /root/.local/share/nvim/plugged \
    && mkdir -p $GOPATH

RUN curl -fLo /root/.local/share/nvim/site/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

COPY myvimrc /root/.config/nvim/init.vim
COPY coc-settings.json /root/.config/nvim/coc-settings.json 


RUN nvim -u /root/.config/nvim/init.vim +PlugInstall +qall

RUN npm install -g yarn

RUN mkdir -p /root/src

WORKDIR /root/src
