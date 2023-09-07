FROM alpine:3.17 as alpine

# Alpine package build

RUN apk --no-cache add alpine-sdk coreutils cmake sudo \
  && adduser -G abuild -g "Alpine Package Builder" -s /bin/ash -D builder \
  && echo "builder ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers \
  && mkdir /packages \
  && chown builder:abuild /packages \
  && mkdir -p /var/cache/apk \
  && ln -s /var/cache/apk /etc/apk/cache

# GCC Toolchain

RUN apk add --quiet --no-cache \
            build-base \
            make \
            cmake \
            gcc

RUN gcc -v

# Gnuradio dependencies

ADD ./etc/apk/repositories /etc/apk/repositories

RUN apk update && \
    apk add --quiet --no-cache \
    isl-dev \
    boost-dev \
    spdlog-dev \
    zeromq-dev \
    cppzmq \
    py3-mako \
    py3-pip \
    python3-dev \
    fftw-dev \
    py3-numpy-dev \
    py3-pybind11-dev \
    py3-pyzmq

RUN echo "/usr/local/lib/python3.10/site-packages" >> /usr/lib/python3.10/site-packages/locallib.pth

RUN mkdir -p /packages && chown builder /packages

USER builder

RUN abuild-keygen -a -i -n

WORKDIR /



