FROM alpine:latest

MAINTAINER Justin Cormack <justin@specialbusservice.com>

RUN \
  apk update && \
  apk upgrade && \
  apk add \
  build-base \
  linux-headers \
  gawk \
  sed \
  zlib-dev \
  openssl-dev \
  ncurses-dev \
  file \
  wget \
  git \
  rsync \
  m4 \
  strace \
  cdrkit \
  coreutils \
  curl

# While still in testing
RUN \
  apk -X http://nl.alpinelinux.org/alpine/edge/testing update && \
  apk -X http://nl.alpinelinux.org/alpine/edge/testing add libseccomp libseccomp-dev

RUN mkdir -p /usr/src && cd /usr/src/ && git clone https://github.com/justincormack/frankenlibc.git

ENV SUDO_UID=1000

RUN \
  cd /usr/src/frankenlibc && \
  LDSTATIC=-static ./build.sh -F CPPFLAGS=-U_FORTIFY_SOURCE -d /usr/local/rump -b /usr/local/bin seccomp && \
  cp rumpobj/tests/hello /usr/local/bin/rump.helloworld && \
  make clean
