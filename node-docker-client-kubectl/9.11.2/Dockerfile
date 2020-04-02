# 基础镜像 node:9.11.2-alpine
FROM node:9.11.2-alpine

# 设置 DOCKER CLI 版本
ARG DOCKER_CLI_VERSION="19.03.8"
ENV DOCKER_CLI_DOWNLOAD_URL="https://download.docker.com/linux/static/stable/x86_64/docker-$DOCKER_CLI_VERSION.tgz"

# 设置 KUBECTL 版本
ARG KUBECTL_VERSION="v1.15.0"
ENV KUBECTL_DOWNLOAD_URL="https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl"

RUN  echo 'http://mirrors.aliyun.com/alpine/v3.10/main' > /etc/apk/repositories \
    && echo 'http://mirrors.aliyun.com/alpine/v3.10/community' >>/etc/apk/repositories \
    && npm config set unsafe-perm true \
    && npm install -g cnpm --registry=https://registry.npm.taobao.org \
    && npm install -g nrm \
    && nrm add transfar http://10.77.0.105:4873/ \
    && apk add --update ca-certificates \
    && apk --update add curl \
    && mkdir -p /tmp/download \
    && curl -L $DOCKER_CLI_DOWNLOAD_URL | tar -xz -C /tmp/download \
    && mv /tmp/download/docker/docker /usr/local/bin/ \
    && rm -rf /tmp/download \
    && curl -L $KUBECTL_DOWNLOAD_URL -o /usr/local/bin/kubectl \
    && chmod +x /usr/local/bin/kubectl \
    && apk del ca-certificates curl \
    && rm -rf /var/cache/apk/*
