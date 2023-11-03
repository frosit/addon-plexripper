# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM=gghcr.io/hassio-addons/base:14.3.1
#ARG BUILD_ARCH=amd64

# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN \
    apk update \
    && apk add \
        dotnet7-sdk \
        git \
        nodejs \
        npm


# Copy root filesystem
COPY rootfs /

# Build arguments

ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION
# RUN \
    # apk add --no-cache --virtual .build-dependencies \