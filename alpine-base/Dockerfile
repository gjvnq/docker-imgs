ARG ALPINE_VERSION=3.16
FROM alpine:${ALPINE_VERSION}
ARG LE_APP_UID=10001
ARG LE_APP_GID=10001

# org.opencontainers.image.authors
# org.opencontainers.image.url
# org.opencontainers.image.documentation
# org.opencontainers.image.source
# org.opencontainers.image.title
# org.opencontainers.image.description
# org.opencontainers.image.ref.name


# Just stuff pretty much every project will likely require
RUN apk add --no-cache \
    curl \
    libcap \
    nano \
    supervisor \
	tzdata

VOLUME /config
VOLUME /data

# Make sure that le_app can write to data but not to /config
RUN addgroup --gid ${LE_APP_GID} le_app && \
	adduser -D -S -s /sbin/nologin -G le_app --uid ${LE_APP_UID} le_app && \
    mkdir /config && \
    mkdir /data && \
    touch /run/supervisord.pid && \
    chown root:le_app /config && \
    chmod 750 /config && \
    chown le_app:le_app /data /run/supervisord.pid && \
    chmod 750 /data