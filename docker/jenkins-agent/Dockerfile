FROM --platform=linux/amd64 jenkins/inbound-agent:3192.v713e3b_039fb_e-1-alpine-jdk21

USER root

RUN apk update && apk add --no-cache \
    unzip \
    git \
    aws-cli \
    terraform

USER jenkins
