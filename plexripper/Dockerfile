# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
#ARG BUILD_FROM=gghcr.io/hassio-addons/base:14.3.1
ARG BUILD_FROM=ghcr.io/home-assistant/amd64-base:3.15
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# hadolint ignore=SC2181, DL3008
RUN apk add --no-cache --virtual .build-dependencies \
        build-base=0.5-r3 \
        py3-pip=23.1.2-r0 \
    \
    && apk add --no-cache \
        dotnet7-sdk \
        git \
        nodejs=18.18.2-r0 \
        npm=9.6.6-r0

RUN pip3 install --no-cache-dir \
        homeassistant-cli==0.9.1 \
    && curl -L -s -o /usr/bin/ha "https://github.com/home-assistant/cli/releases/download/4.29.0/ha_${BUILD_ARCH}" \
    && chmod a+x /usr/bin/ha

# Cleanup
RUN apk del --no-cache --purge .build-dependencies \
        && rm -fr \
            /tmp/* \
            /root/.cache

# Copy root filesystem
COPY rootfs /

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION