FROM gcr.io/stacksmith-images/minideb:jessie-r10

MAINTAINER Bitnami <containers@bitnami.com>

ENV BITNAMI_APP_NAME=rabbitmq \
    BITNAMI_IMAGE_VERSION=3.6.6-r7 \
    PATH=/opt/bitnami/erlang/bin:/opt/bitnami/rabbitmq/sbin:/opt/bitnami/rabbitmq/bin:$PATH

# System packages required
RUN install_packages --no-install-recommends libc6 libssl1.0.0 libtinfo5 zlib1g

# Additional modules required
RUN bitnami-pkg install erlang-17.4-3 --checksum 7465a1ac11bf98cc1e2a549758dd4fccb2812d60ede33d1f68e0c7ec312b0b88

# Install rabbitmq
RUN bitnami-pkg unpack rabbitmq-3.6.6-2 --checksum a45b57ff8ba832ef005721f120270c0054fcf134d2a9925f27ef3c9be0002299

COPY rootfs /

ENV RABBITMQ_VHOST="/" \
    RABBITMQ_USERNAME="user" \
    RABBITMQ_PASSWORD="bitnami" \
    RABBITMQ_NODE_TYPE="stats" \
    RABBITMQ_NODE_PORT="5672" \
    RABBITMQ_NODE_NAME="rabbit@localhost" \
    RABBITMQ_MANAGER_PORT="15672"

VOLUME ["/bitnami/rabbitmq"]

EXPOSE 4369 5672 25672 15672

ENTRYPOINT ["/app-entrypoint.sh"]

CMD ["nami", "start", "--foreground", "rabbitmq"]
