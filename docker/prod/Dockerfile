FROM ruby:3.1.2-slim

ENV APP_ROOT /myapp

RUN mkdir $APP_ROOT
WORKDIR $APP_ROOT

RUN apt-get update -qq && apt-get install -yq --no-install-recommends \
    build-essential \
    gnupg2 \
    less \
    git \
    telnet \
    nodejs \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN apt-get update -qq && apt-get install -y default-libmysqlclient-dev

#Cache bundle install
ADD ./Gemfile Gemfile
ADD ./Gemfile.lock Gemfile.lock

RUN gem update --system \
    && bundle update --bundler \
    && bundle config set --local without 'development test' \
    && bundle install \

COPY . $APP_ROOT


EXPOSE  3000

CMD rm -f tmp/pids/server.pid && rails s -b '0.0.0.0'