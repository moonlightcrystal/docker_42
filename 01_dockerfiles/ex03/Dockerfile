FROM debian:stable

ENV DEBIAN_FRONTEND=noninteractive
ENV TERM=xterm
ARG GITLAB_IP=localhost

RUN apt-get update -y && \
	apt-get upgrade -y && \
	apt-get install -y curl openssh-server ca-certificates git tzdata


#install gitlab repo
RUN curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash

#install package Gitlab

RUN apt-get update -y && apt-get install -y --no-install-recommends gitlab-ce

# Create self-signed certificate

RUN mkdir -p /etc/gitlab/ssl && \
	chmod 700 /etc/gitlab/ssl && \
	openssl req -new -x509 -nodes -newkey rsa:2048 -keyout /etc/gitlab/ssl/gitlab.key -out /etc/gitlab/ssl/gitlab.crt -days 365 -subj /CN=${GITLAB_IP} && \
	sed -i -e "s|^\(external_url\) .*$|\1 'https://${GITLAB_IP}'|" \
	-e "s|^# \(nginx\['ssl_certificate'\] = \"/etc/gitlab/ssl\)/.*$|\1/gitlab.crt\"|" \
	-e "s|^# \(nginx\['ssl_certificate_key'\] = \"/etc/gitlab/ssl\)/.*$|\1/gitlab.key\"|" \
	-e "s|^# \(gitlab_rails\['gitlab_shell_ssh_port'\] = 22\)$|\1|" \
	/etc/gitlab/gitlab.rb

EXPOSE 443
EXPOSE 22

ENTRYPOINT  service ssh start && \
				(/opt/gitlab/embedded/bin/runsvdir-start &) && \
				gitlab-ctl reconfigure && \
				gitlab-ctl tail

#see your ip
#step1 docker build --build-arg GITLAB_IP=(docker-machine ip Char) -t gitlab .
#docker build --build-arg GITLAB_IP=192.168.99.113 -t gitlab .
#docker run --rm -it -p 8000:443 -p 8022:22 --privileged gitlab 

