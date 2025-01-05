FROM golang

RUN apt-get update && \
    apt-get install -y vim git && \
    mkdir -p ~/.vim/autoload && \
    curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim && \
    git clone https://github.com/fatih/vim-go.git ~/.vim/plugged/vim-go

COPY myvimrc /root/.vimrc

# Vimを起動してプラグインをインストール
RUN vim -c "source ~/.vimrc" -c "PlugInstall" -c "GoInstallBinaries" -c "qa!"

# コンテナ起動時にvimを実行したい場合は、CMDを指定
CMD ["vim"] 