FROM alpine:3.5

MAINTAINER Rui Carmo https://github.com/rcarmo

# Adds testing package to repositories
# Install needed packages. Notes:
#   * build-base: used so we include the basic development packages (gcc)
#   * python-dev: are used for gevent e.g.
#   * bash: so we can access /bin/bash
RUN echo "@testing http://dl-4.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
 && apk add --update \
              ca-certificates \
              musl \
              build-base \
              python3 \
              python3-dev \
              bash \
              git \
              gfortran \
              lapack-dev \
              libxml2-dev \
              libxslt-dev \
              jpeg-dev \
 && pip3.5 install --upgrade pip \
 && rm /var/cache/apk/*

# make us compatible with manylinux wheels and create some useful symlinks that are expected to exist
RUN echo "manylinux1_compatible = True" > /usr/lib/python3.5/_manylinux.py \
 && cd /usr/bin \
 && ln -sf easy_install-3.5 easy_install \
 && ln -sf idle3.5 idle \
 && ln -sf pydoc3.5 pydoc \
 && ln -sf python3.5 python \
 && ln -sf python-config3.5 python-config \
 && ln -sf pip3.5 pip \
 && ln -sf /usr/include/locale.h /usr/include/xlocale.h

# since we will be "always" mounting the volume, we can set this up
CMD python
