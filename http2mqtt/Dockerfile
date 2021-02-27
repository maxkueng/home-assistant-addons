ARG BUILD_FROM=ghcr.io/hassio-addons/base/amd64:9.1.3

FROM ${BUILD_FROM}

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN \
  apk add --no-cache --virtual .build-dependencies \
    npm=14.16.0-r0 \
  \
  && apk add --no-cache \
  nodejs=14.16.0-r0 \
  \
  && curl -J -L -o /tmp/http2mqtt.tar.gz \
    "https://github.com/maxkueng/http2mqtt/archive/2bfe5a4f81eeefcd31d24c9dfc23070f8e68397a.tar.gz" \
  && tar zxvf \
    /tmp/http2mqtt.tar.gz \
    --strip 1 -C /opt \
  \
  && cd /opt \
  && npm config set unsafe-perm \
  && npm install \
  && npm run build \
  && npm prune --production \
  \
  && apk del --no-cache --purge .build-dependencies \
  && rm -f -r \
    /root/.node-gyp \
    /root/.npm \
    /tmp/.[!.]* \
    /tmp/* \
    /usr/lib/node_modules \
    /usr/local/share/.cache

# Copy root filesystem
COPY rootfs /

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

EXPOSE 8321

# Labels
LABEL \
    io.hass.name="HTTP to MQTT" \
    io.hass.description="A bridge to connect HTTP-based IoT devices to MQTT" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Max Kueng (https://maxkueng.com/contact)" \
    org.label-schema.description="A bridge to connect HTTP-based IoT devices to MQTT" \
    org.label-schema.build-date=${BUILD_DATE} \
    org.label-schema.name="HTTP to MQTT" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.url="https://github.com/maxkueng/hassio-http2mqtt" \
    org.label-schema.usage="https://github.com/maxkueng/hassio-http2mqtt/tree/master/README.md" \
    org.label-schema.vcs-ref=${BUILD_REF} \
    org.label-schema.vcs-url="https://github.com/maxkueng/hassio-http2mqtt" \
    org.label-schema.vendor="Home Assistant Community Add-ons"

