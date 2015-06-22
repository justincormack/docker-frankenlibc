FROM ubuntu:14.04

MAINTAINER Justin Cormack <justin@specialbusservice.com>

RUN \
  apt-get update && \
  apt-get upgrade -y && \
  apt-get install -y \
  build-essential \
  git \
  libseccomp2 \
  libseccomp-dev \
  clang \
  gcc-arm-none-eabi \
  gcc-arm-linux-gnueabihf

RUN mkdir -p /usr/src && cd /usr/src/ && git clone https://github.com/justincormack/frankenlibc.git

ENV \
  SUDO_UID=1000

RUN \
  cd /usr/src/frankenlibc && \
  ./build.sh -d /usr/local/rump -b /usr/local/bin seccomp && \
  cp rumpobj/tests/hello /usr/local/bin/rump.helloworld && \
  make clean
