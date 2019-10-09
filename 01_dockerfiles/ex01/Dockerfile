FROM debian

MAINTAINER treshotka <weloveyoucris7@gmail.com>

ENV TS3SERVER_LICENSE=accept

WORKDIR /home/teamspeak

EXPOSE 9987/udp 30033 10011

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y wget && \
    apt-get install -y bzip2 && \
    wget https://files.teamspeak-services.com/releases/server/3.9.1/teamspeak3-server_linux_amd64-3.9.1.tar.bz2 && \
    tar xvf teamspeak3-server_linux_amd64-3.9.1.tar.bz2

WORKDIR teamspeak3-server_linux_amd64

ENTRYPOINT ./ts3server_minimal_runscript.sh




