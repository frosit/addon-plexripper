# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM=gghcr.io/hassio-addons/base:14.3.1

# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Copy Python requirements file
COPY requirements.txt /tmp/

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

ARG BUILD_ARCH=amd64
RUN \
    apk update \
    && apk add \
        dotnet7-sdk \
        git \
        nodejs \
        npm \
        py3-pip=20.3.4-r1 \
        python3=3.9.5-r1 \
        bash-completion=2.11-r4 \
    && curl -L -s -o /usr/bin/ha \
        "https://github.com/home-assistant/cli/releases/download/4.29.0/ha_${BUILD_ARCH}" \
    \
    && chmod a+x /usr/bin/ha \
    && ha completion > /usr/share/bash-completion/completions/ha  \
    \
    && pip3 install \
        --no-cache-dir \
        --find-links "https://wheels.home-assistant.io/alpine-3.14/${BUILD_ARCH}/" \
        -r /tmp/requirements.txt \
    \
    && hass-cli completion bash > /usr/share/bash-completion/completions/hass-cli \
    \
    && apk del --no-cache --purge .build-dependencies \
    \
    && find /usr/local \
        \( -type d -a -name test -o -name tests -o -name '__pycache__' \) \
        -o \( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
        -exec rm -rf '{}' + \
    \
    && rm -f -r \
        /root/.cache \
        /root/.cmake \
        /tmp/*

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