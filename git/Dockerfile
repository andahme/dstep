ARG INPUT_DOCKER_REGISTRY=andahme



FROM ${INPUT_DOCKER_REGISTRY}/debian:base AS git


RUN apt-get update && \
    apt-get install --yes --no-install-recommends ca-certificates git openssh-client

RUN useradd --comment "Git User" --create-home --uid 1011 git && \
    mkdir /workspace && \
    chown git /workspace


WORKDIR /workspace

USER git

