FROM centos:centos7

MAINTAINER Justin Cormack <justin@specialbusservice.com>

RUN \
  yum install -y \
  git \
  libseccomp-devel \
  libsseccomp \
  clang \
  && \
  yum groupinstall -y "Development Tools"

RUN mkdir -p /usr/src && cd /usr/src/ && git clone https://github.com/justincormack/frankenlibc.git

ENV \
  SUDO_UID=1000

RUN \
  cd /usr/src/frankenlibc && \
  ./build.sh -d /usr/local/rump -b /usr/local/bin seccomp && \
  cp rumpobj/tests/hello /usr/local/bin/rump.helloworld && \
  make clean
