FROM ubuntu:latest

# 共通の依存関係をインストール
RUN apt-get update -y \
    && apt-get install -y \
    software-properties-common \
    curl \
    git \
    build-essential \
    python3 \
    python3-pip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Goをインストール
RUN add-apt-repository ppa:longsleep/golang-backports -y \
    && apt-get update -y \
    && apt-get install -y golang-go \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Node.jsとnpmをインストール
RUN curl -sL https://deb.nodesource.com/setup_lts.x | bash - \
    && apt-get update -y \
    && apt-get install -y nodejs \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# NeovimをPPAからインストール (stable版)
RUN add-apt-repository ppa:neovim-ppa/stable -y \
    && apt-get update -y \
    && apt-get install -y neovim \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# --- または ---
# NeovimをPPAからインストール (unstable版 - 最新版だが安定性は低い)
# RUN add-apt-repository ppa:neovim-ppa/unstable -y \
#     && apt-get update -y \
#     && apt-get install -y neovim \
#     && apt-get clean \
#     && rm -rf /var/lib/apt/lists/*


ENV GOPATH=/root/go
ENV PATH=$PATH:/usr/local/go/bin:$GOPATH/bin
ENV NODE_ENV=development

# 必要なディレクトリを作成
RUN mkdir -p $GOPATH \
    && mkdir -p /root/.config/nvim/ \
    && mkdir -p /root/.local/share/nvim/site/autoload

# vim-plugをインストール
RUN curl -fLo /root/.local/share/nvim/site/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

# 設定ファイルをコピー
COPY myvimrc /root/.config/nvim/init.vim
COPY coc-settings.json /root/.config/nvim/coc-settings.json

# Neovimプラグインをインストール
RUN nvim -u /root/.config/nvim/init.vim +PlugInstall +qall

# yarnをグローバルインストール
RUN npm install -g yarn

# srcディレクトリを作成
RUN mkdir -p /root/src

WORKDIR /root/src