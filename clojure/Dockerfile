FROM ubuntu:latest

RUN apt-get update && \
    apt-get install -y zsh openssh-server git gdebi wget emacs software-properties-common

RUN apt-add-repository ppa:webupd8team/java && \
    apt-get update && \
    echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
    apt-get install -y oracle-java8-installer

#oh-my-zsh, because how do we live without it?
RUN git clone https://github.com/robbyrussell/oh-my-zsh.git

ADD ./deps/.zshrc /root/.zshrc
ADD ./deps/lovelace.zsh-theme /oh-my-zsh/themes/lovelace.zsh-theme

#lein installation
ENV LEIN_ROOT=1
RUN cd /usr/local/bin/ && wget https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein && chmod +x ./lein

RUN lein

WORKDIR /code