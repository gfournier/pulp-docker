FROM python:3.8-alpine
MAINTAINER Guillaume Fournier <fournierg@gmail.com>

ENV CBC_VERSION 2.10.5

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
  && ./coinbrew build Cbc FFLAGS=-fallow-argument-mismatch -n -b ./build -p /usr/local \
#  && cd / \
  && apk del --no-network .build-deps \
  && apk add --no-cache \
      libblas \
      liblapack \
      libstdc++ \
      libgfortran
#  && rm -rf ./build_dir

# Install pulp package and replace default cbc binary since it's not valid in alpine
RUN pip install pulp \
  && rm /usr/local/lib/python3.8/site-packages/pulp/solverdir/cbc/linux/64/cbc \
  && ln -s /usr/local/bin/cbc /usr/local/lib/python3.8/site-packages/pulp/solverdir/cbc/linux/64/cbc

# ENV PATH="/dist/bin:${PATH}"

CMD ["/bin/sh"]
