# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM=gghcr.io/hassio-addons/base:14.3.1
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Execute during the build of the image
ARG TEMPIO_VERSION BUILD_ARCH

RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"


RUN \
    apk add --no-cache --virtual .build-dependencies \
        build-base=0.5-r3 \
        py3-pip=23.1.2-r0 \
    \
    && apk add --no-cache \
        dotnet7-sdk \
        git \
        nodejs=18.18.2-r0 \
        npm=9.6.6-r0  \
    \
        && curl -L -s -o /usr/bin/ha \
            "https://github.com/home-assistant/cli/releases/download/4.12.3/ha_${BUILD_ARCH}" \
        \
        && chmod a+x /usr/bin/ha \
        && ha completion > /usr/share/bash-completion/completions/ha




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
# RUN \
    # apk add --no-cache --virtual .build-dependencies \