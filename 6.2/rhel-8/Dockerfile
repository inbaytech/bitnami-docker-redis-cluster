FROM registry.access.redhat.com/ubi8/ubi-minimal
#ARG uid=1001
ENV REDIS_VERSION=6.2.6-8 \
    BITNAMI_RELEASE=r68 \
    HOME="/" \
    OS_ARCH="amd64" \
    OS_FLAVOUR="rhel-8" \
    OS_NAME="linux"

COPY prebuildfs /
# Install required system packages and dependencies
RUN install_packages acl ca-certificates curl gzip procps shadow-utils tar
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "redis" "${REDIS_VERSION}" --checksum 611d29fa780a94ecd65cd0a2a6176e94075f8d358047f10f1097d055032a7144
RUN curl -o /usr/local/bin/gosu https://github.com/tianon/gosu/releases/download/1.14/gosu-amd64

COPY rootfs /
RUN /opt/bitnami/scripts/redis-cluster/postunpack.sh
ENV BITNAMI_APP_NAME="redis-cluster" \
    BITNAMI_IMAGE_VERSION="${REDIS_VERSION}-rhel-8-${BITNAMI_RELEASE}" \
    PATH="/opt/bitnami/redis/bin:/opt/bitnami/common/bin:$PATH"

EXPOSE 6379

ENTRYPOINT [ "/opt/bitnami/scripts/redis-cluster/entrypoint.sh" ]
CMD [ "/opt/bitnami/scripts/redis-cluster/run.sh" ]
