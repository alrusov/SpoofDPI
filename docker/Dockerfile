FROM ubuntu:22.04

ARG BUILD_HOME
ARG APP_HOME
ARG APP
ARG PORT
ARG DOCKER_UID
ARG DOCKER_USER
ARG DOCKER_GID
ARG DOCKER_GROUP

ENV PORT=9999

COPY ${BUILD_HOME}/ ${APP_HOME}/

RUN \
  apt update -y && \
  apt upgrade -y && \
  apt clean && \
  addgroup --gid ${DOCKER_GID} ${DOCKER_GROUP}; \
  adduser --home ${APP_HOME} --gecos ${DOCKER_USER} --uid ${DOCKER_UID} --ingroup ${DOCKER_GROUP} --shell /bin/bash --disabled-password ${DOCKER_USER}; \
  chown -R ${DOCKER_USER}:${DOCKER_GROUP} ${APP_HOME} && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

USER ${DOCKER_USER}

WORKDIR ${APP_HOME}

ENTRYPOINT ./spoof-dpi -addr 0.0.0.0 -port $PORT
