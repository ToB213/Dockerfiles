 FROM golang

RUN apt-get update && \
    apt-get install -y vim git && \
    mkdir -p ~/.vim/autoload && \
    curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim && \
    git clone https://github.com/fatih/vim-go.git ~/.vim/plugged/vim-go

COPY myvimrc /root/.vimrc

# Vimを起動してプラグインをインストール
RUN vim -Es -u NONE -c "source $HOME/.vimrc" -c "PlugInstall --sync | exit 0"  -c "qa!"

# コンテナ起動後に以下のコマンドが必要
# vim -c "GoInstallBinaries"