FROM debian:9.9

MAINTAINER treshotka <weloveyoucris7@gmail.com>

RUN apt-get update -y && apt-get upgrade -y && apt-get install -y \
  openssh-server && \
  apt-get install -y emacs && \  
  apt-get install -y build-essential git && \
  rm -rf /var/lib/apt/lists/*

RUN echo 'root:password' | chpasswd

RUN mkdir /var/run/sshd

RUN sed 's/PermitRootLogin without-password/PermitRootLogin yes/' -i /etc/ssh/sshd_config

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
