ARG BUILD_FROM
FROM $BUILD_FROM


# Copy root filesystem
COPY rootfs /

# Setup requirements
ARG BUILD_ARCH
env BUILD_ARCH $BUILD_ARCH

RUN set -x \
    && apk add --no-cache curl \
    && if [[ "${BUILD_ARCH}" = "aarch64" ]]; then ARCH="arm64"; fi \
    && if [[ "${BUILD_ARCH}" = "amd64" ]]; then ARCH="amd64"; fi \
    && if [[ "${BUILD_ARCH}" = "armhf" ]]; then ARCH="arm"; fi \
    && if [[ "${BUILD_ARCH}" = "armv7" ]]; then ARCH="arm"; fi \
    && if [[ "${BUILD_ARCH}" = "i386" ]]; then ARCH="386"; fi
RUN apk add --no-cache openssh file libc6-compat
RUN ssh-keygen -b 2048 -t rsa -f /root/.ssh/id_rsa -q -N ""

COPY run.sh /
RUN chmod a+x /run.sh
CMD [ "/run.sh" ]
