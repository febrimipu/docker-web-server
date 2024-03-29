FROM bitnami/oraclelinux-extras-base:7-r303
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV BITNAMI_PKG_CHMOD="-R g+rwX" \
    HOME="/" \
    OS_ARCH="x86_64" \
    OS_FLAVOUR="ol-7" \
    OS_NAME="linux" \
    TIMEZONE="Asia/Jakarta"

# Install required system packages and dependencies
RUN install_packages cyrus-sasl-lib glibc keyutils-libs krb5-libs libaio libcom_err libgcc libselinux libstdc++ ncurses-libs nss-softokn-freebl pcre
RUN . ./libcomponent.sh && component_unpack "mysql" "5.7.26-0" --checksum 90488b362ca049f58bc4dd0f48d418bf4119d779d0ad442b97f725f02e708e83
RUN mkdir /docker-entrypoint-initdb.d

COPY rootfs /
RUN /postunpack.sh
ENV ALLOW_EMPTY_PASSWORD="no" \
    BITNAMI_APP_NAME="mysql" \
    BITNAMI_IMAGE_VERSION="5.7.26-ol-7-r37" \
    MYSQL_DATABASE="" \
    MYSQL_MASTER_HOST="" \
    MYSQL_MASTER_PORT_NUMBER="" \
    MYSQL_MASTER_ROOT_PASSWORD="" \
    MYSQL_MASTER_ROOT_USER="" \
    MYSQL_PASSWORD="" \
    MYSQL_PORT_NUMBER="3306" \
    MYSQL_REPLICATION_MODE="" \
    MYSQL_REPLICATION_PASSWORD="" \
    MYSQL_REPLICATION_USER="" \
    MYSQL_ROOT_PASSWORD="" \
    MYSQL_ROOT_USER="root" \
    MYSQL_USER="" \
    NAMI_PREFIX="/.nami" \
    PATH="/opt/bitnami/mysql/bin:$PATH"

RUN rm -f /etc/localtime
RUN ln -s /usr/share/zoneinfo/$TIMEZONE /etc/localtime
RUN date

EXPOSE 3306

USER 1001
ENTRYPOINT [ "/entrypoint.sh" ]
CMD [ "/run.sh" ]
