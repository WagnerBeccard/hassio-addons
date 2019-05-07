ARG BUILD_FROM=hassioaddons/ubuntu-base:3.1.1
FROM $BUILD_FROM

ARG BUILD_ARCH
ARG BUILD_VERSION

LABEL maintainer "Philipp Schmitt <philipp@schmitt.co>"

# Install the fliclib-linux-hci
RUN \
    apt-get update \
    \
    && apt-get install -y --no-install-recommends \
        git \
    git clone https://github.com/50ButtonsEach/fliclib-linux-hci /tmp/src && \
    cp /tmp/src/bin/${ARCH}/flicd /usr/bin/flicd && \
    chmod +x /usr/bin/flicd && \
    mkdir /config && \
    rm -rf /tmp/src && \
    apt-get remove --purge -y git && \
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /data
VOLUME ["/data"]
EXPOSE 5551
ENTRYPOINT ["/usr/bin/flicd"]
CMD ["-f", "/data/flic-db", "-s", "0.0.0.0", "-p", "5551"]

# Build arguments
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="Flicd" \
    io.hass.description="Flic service for hass.io" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="none>" \
    org.label-schema.description="Flic service for hass.io." \
    org.label-schema.build-date=${BUILD_DATE} \
    org.label-schema.name="Flicd" \
    org.label-schema.schema-version="0.01" \
    org.label-schema.url="hhttps://github.com/WagnerBeccard/hassio-addons/" \
    org.label-schema.usage="hhttps://github.com/WagnerBeccard/hassio-addons/tree/master/README.md" \
    org.label-schema.vcs-ref=${BUILD_REF} \
    org.label-schema.vcs-url="https://github.com/WagnerBeccard/hassio-addons/" \
    org.label-schema.vendor="Community Hass.io Add-ons"
