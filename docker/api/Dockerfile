ARG RUBY_PATH=/usr/local/
ARG RUBY_VERSION=3.0.2

FROM localdev/docker-ruby-image:latest AS rubybuild

FROM ubuntu:20.04
ARG RUBY_PATH
ENV PATH $RUBY_PATH/bin:$PATH
ENV LANG=ja_JP.UTF-8
ENV APP_ROOT=/usr/app
# [apt-get(8) - Linux man page](https://linux.die.net/man/8/apt-get)
# 出力されるlogを少なくする
RUN apt-get update && apt-get upgrade
RUN apt-get install -y --no-install-recommends \
  autoconf \
  bison \
  build-essential \
  bzip2 \
  ca-certificates \
  curl \
  git \
  libreadline-dev \
  libmysqlclient-dev \
  libssl-dev \
  libyaml-dev \
  libreadline6-dev \
  libncurses5-dev \
  libffi-dev \
  libgdbm-dev \
  zlib1g-dev

COPY --from=rubybuild $RUBY_PATH $RUBY_PATH

RUN mkdir $APP_ROOT

WORKDIR $APP_ROOT

# アプリのコードを追加
ADD ./backendVolume $APP_ROOT
RUN gem update --system && \
  gem install bundler rails && \
  bundle install
