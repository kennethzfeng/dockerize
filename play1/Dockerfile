FROM java:7

MAINTAINER Kenneth Feng <ken@kfeng.me>

RUN apt-get update && apt-get install -y sudo ant python && apt-get clean

ENV HOME /opt/play
ENV PLAY_VERSION 1.4.2

RUN groupadd -r play -g 1000 && \
    useradd -u 1000 -r -g play -m -d $HOME -s /sbin/nologin -c "Play user" play

WORKDIR $HOME
USER play

RUN wget -q https://downloads.typesafe.com/play/${PLAY_VERSION}/play-${PLAY_VERSION}.zip && \
    unzip -q play-${PLAY_VERSION}.zip && rm play-${PLAY_VERSION}.zip && cd play-${PLAY_VERSION}

RUN sed 's#www.playframework.com#'"playframework.com"'#' -i $HOME/play-${PLAY_VERSION}/framework/dependencies.yml

USER root
RUN ln -sf $HOME/play-${PLAY_VERSION}/play /usr/local/bin
USER play

EXPOSE 9000
