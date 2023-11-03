# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM=gghcr.io/hassio-addons/base:14.3.1

# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Copy Python requirements file
COPY requirements.txt /tmp/

# hadolint ignore=SC2181, DL3008
RUN \
    apk update \
    && apk add \
        dotnet7-sdk \
        git \
        nodejs \
        npm \
        py3-pip \
        python3 \
        bash-completion

ARG BUILD_ARCH=amd64
RUN curl -L -s -o /usr/bin/ha "https://github.com/home-assistant/cli/releases/download/4.29.0/ha_${BUILD_ARCH}"
RUN chmod a+x /usr/bin/ha
RUN ha completion > /usr/share/bash-completion/completions/ha

RUN pip3 install homeassistant_cli==0.9.1

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

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