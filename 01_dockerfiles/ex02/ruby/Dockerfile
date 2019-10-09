FROM ruby:2.3.1-slim

MAINTAINER treshotka <weloveyoucris7@gmail.com>

RUN apt-get update -y && \
    apt-get install -y build-essential libcurl4-openssl-dev libxml2-dev libsqlite3-dev libpq-dev nodejs postgresql-client sqlite3 --no-install-recommends && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


ONBUILD COPY appp /opt/app

ONBUILD WORKDIR /opt/app

ONBUILD RUN bundle config --global frozen 1
ONBUILD EXPOSE 3000
ONBUILD RUN bundle install
ONBUILD RUN rake db:migrate
ONBUILD RUN rake db:seed
ONBUILD RUN rake assets:precompile

#USE
#docker build -t ft-rails:on-build .