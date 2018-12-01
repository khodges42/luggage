FROM ubuntu:latest

RUN apt-get update && \
    apt-get install -y zsh openssh-server git gdebi wget emacs software-properties-common

#oh-my-zsh, because how do we live without it?
RUN git clone https://github.com/robbyrussell/oh-my-zsh.git

ADD ./deps/.zshrc /root/.zshrc
ADD ./deps/lovelace.zsh-theme /oh-my-zsh/themes/lovelace.zsh-theme

WORKDIR /code