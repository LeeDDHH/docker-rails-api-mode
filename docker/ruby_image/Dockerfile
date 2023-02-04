ARG RUBY_PATH=/usr/local/
ARG RUBY_VERSION=3.0.2

FROM ubuntu:20.04

ARG RUBY_PATH
ARG RUBY_VERSION

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

RUN git clone https://github.com/rbenv/ruby-build.git $RUBY_PATH/plugins/ruby-build \
&&  $RUBY_PATH/plugins/ruby-build/install.sh
RUN ruby-build $RUBY_VERSION $RUBY_PATH
