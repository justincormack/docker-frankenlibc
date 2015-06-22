# Not currently being built due to constructor test failing

FROM centos:centos6

MAINTAINER Justin Cormack <justin@specialbusservice.com>

RUN \
  yum update -y && \
  yum install -y \
  git \
  tar \
  && \
  yum groupinstall -y "Development Tools"

RUN mkdir -p /usr/src && cd /usr/src/ && git clone https://github.com/justincormack/frankenlibc.git

ENV \
  SUDO_UID=1000

RUN \
  cd /usr/src/frankenlibc && \
  ./build.sh -d /usr/local/rump -b /usr/local/bin && \
  cp rumpobj/tests/hello /usr/local/bin/rump.helloworld && \
  make clean
