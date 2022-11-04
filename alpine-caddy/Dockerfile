ARG ALPINE_VERSION=3.16
FROM alpine:${ALPINE_VERSION}
ARG LE_APP_UID=10001
ARG LE_APP_GID=10001

RUN apk add --no-cache \
    caddy \
    curl \
    libcap \
	tzdata

EXPOSE 80
VOLUME /config
VOLUME /srv

COPY Caddyfile /config/Caddyfile

RUN addgroup --gid ${LE_APP_GID} le_app && \
	adduser -D -S -s /sbin/nologin -G le_app --uid ${LE_APP_UID} le_app && \
	setcap cap_net_bind_service=+ep `readlink -f /usr/sbin/caddy` && \
	chown le_app:le_app /srv

USER le_app

CMD ["caddy", "run", "--config", "/config/Caddyfile"]