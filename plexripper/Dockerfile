# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
#ARG BUILD_FROM=ghcr.io/home-assistant/amd64-base:3.15
ARG BUILD_FROM
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# hadolint ignore=SC2181, DL3008
RUN apk add --no-cache --virtual .build-dependencies \
        build-base \
        py3-pip \
    \
    && apk add --no-cache \
        dotnet8-sdk \
        git \
        nodejs \
        npm

ENV DOTNET_ENVIRONMENT=Production
ENV ASPNETCORE_URLS=http://+:7000
ENV DOTNET_URLS=http://+:7000
ENV VERSION=0.0.0
ENV NUXT_HOST=0.0.0.0
ENV NUXT_PORT=7000
ENV API_PORT=7000
ENV NUXT_PUBLIC_IS_DOCKER=true

RUN git clone https://github.com/plexripper/plexripper /tmp/plexripper \
    && cd /tmp/plexripper/src/WebAPI \
    && dotnet publish "WebAPI.csproj" -c Release -o /opt/plexripper /p:AssemblyVersion=${VERSION} \
    && cd /tmp/plexripper/src/WebAPI/ClientApp \
    && npm install \
    && npm run generate --fail-on-error \
    && rm -Rf /opt/plexripper/ClientApp \
    && cp -R /tmp/plexripper/src/WebAPI/ClientApp /opt/plexripper/ClientApp \
    && ln -s /opt/plexripper/ClientApp/.output/public /opt/plexripper/wwwroot

#ARG BUILD_ARCH=amd64
#RUN pip3 install --no-cache-dir \
#        homeassistant-cli==0.9.1 \
#    && curl -L -s -o /usr/bin/ha "https://github.com/home-assistant/cli/releases/download/4.29.0/ha_${BUILD_ARCH}" \
#    && chmod a+x /usr/bin/ha

# Cleanup
RUN apk del --no-cache --purge .build-dependencies \
        && rm -fr \
            /tmp/* \
            /root/.cache

# Copy root filesystem
COPY rootfs /
