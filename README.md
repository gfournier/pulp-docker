# Pulp Dockerfile

This is a Docker image containing a rebuilt version of COIN-OR optimization suite
and the [Pulp](https://github.com/coin-or/pulp) Python package for Alpine Linux.

A Docker image for Ubuntu is available and maintained by COIN-OR [here](https://github.com/coin-or-tools/optimization-suite-docker).

## Install and use from Docker Hub

Pull image from [Docker Hub](https://hub.docker.com/r/gfournier/pulp/tags).

```
docker pull pulp:3.8-alpine
```

Then start a container on this image.
```
docker run -it pulp:3.8-alpine
```

And run the pulp test suite which should pass.
```
pulptest
```

## Build image locally

You must have a valid Docker installation. Then run following commands:

```
git clone https://github.com/gfournier/pulp-docker
cd pulp-docker
docker build -t pulp alpine/
```

Then start a container and run test (see previous section).
