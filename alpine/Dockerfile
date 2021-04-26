FROM python:3.8-alpine
MAINTAINER Guillaume Fournier <fournierg@gmail.com>

ENV CBC_VERSION 2.10.5

ENV PATH="/dist/bin:${PATH}"

RUN apk add --no-cache --virtual .build-deps \
      bash \
      git \
      patch \
      pkgconf \
      build-base \
      gfortran \
      lapack-dev \
      blas-dev \
  && mkdir build_dir \
  && cd build_dir \
  && wget https://raw.githubusercontent.com/coin-or/coinbrew/master/coinbrew \
  && chmod u+x coinbrew \
  && ./coinbrew fetch "Cbc@releases/$CBC_VERSION" \
  && ./coinbrew build Cbc FFLAGS=-fallow-argument-mismatch --no-prompt --tests none --verbosity 3 --build-dir ./build --prefix /dist \
  && cd / \
  && apk del --no-network .build-deps \
  && rm -rf ./build_dir \
  && apk add --no-cache \
      lapack \
      openblas \
      libgfortran \
      libstdc++ \
  && pip install pulp \
  && rm /usr/local/lib/python3.8/site-packages/pulp/solverdir/cbc/linux/64/cbc \
  && ln -s /dist/bin/cbc /usr/local/lib/python3.8/site-packages/pulp/solverdir/cbc/linux/64/cbc \
  && pulptest

CMD ["/bin/sh"]
