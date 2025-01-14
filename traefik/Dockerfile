#################
# 1 Build Image #
#################
ARG BUILD_FROM
FROM $BUILD_FROM

ARG BUILD_ARCH
ARG TRAEFIK_VERSION


##################
# 2 Modify Image #
##################
RUN if [ "${BUILD_ARCH}" == "aarch64" ]; then BUILD_ARCH=arm64; \
    elif [ "${BUILD_ARCH}" == "i386" ]; then BUILD_ARCH=386; \
    elif [ "${BUILD_ARCH}" == "armhf" ]; then BUILD_ARCH=armv7; \
    fi && \
    apk add --no-cache nginx gomplate && \
    wget --quiet -O /tmp/traefik.tar.gz "https://github.com/traefik/traefik/releases/download/v${TRAEFIK_VERSION}/traefik_v${TRAEFIK_VERSION}_linux_${BUILD_ARCH}.tar.gz" && \
    tar xzvf /tmp/traefik.tar.gz -C /usr/local/bin traefik && \
    chmod +x /usr/local/bin/traefik && \
    rm -f /tmp/*


##################
# 3 Install apps #
##################
# Add rootfs
COPY rootfs /


############
# 4 Labels #
############

ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

RUN echo "Traefik version: ${TRAEFIK_VERSION} ${BUILD_ARCH}"
RUN echo "Date: ${BUILD_DATE}"
RUN echo "Ref: ${BUILD_REF}"
RUN echo "Repo: ${BUILD_REPOSITORY}"
RUN echo "Version: ${BUILD_VERSION}"

LABEL \
    io.hass.name="Treafik for ${BUILD_ARCH}" \
    io.hass.description="Home Assistant Unofficial Add-on: ${BUILD_ARCH} Traefik image" \
    maintainer="Alex van den Hoogen <homeassistant@alxx.nl>" \
    org.opencontainers.image.title="Traefik for ${BUILD_ARCH}" \
    org.opencontainers.image.description="Home Assistant Unofficial Add-on: ${BUILD_ARCH} Traefik image" \
    org.opencontainers.image.vendor="Alex van den Hoogen" \
    org.opencontainers.image.authors="Alex van den Hoogen <homeassistant@alxx.nl>" \
    org.opencontainers.image.url="https://alxx.nl/home-assistant-addons/" \
    org.opencontainers.image.source="https://alxx.nl/home-assistant-addons/" \
    org.opencontainers.image.documentation="https://alxx.nl/home-assistant-addons/blob/master/traefik/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
