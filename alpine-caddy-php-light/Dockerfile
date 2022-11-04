#TODO: reduce number of installed packages
ARG ALPINE_VERSION=3.16
FROM alpine:${ALPINE_VERSION}
ARG LE_APP_UID=10001
ARG LE_APP_GID=10001

# This list mostly comes from MediaWiki, Wordpress and Drupal
RUN apk add --no-cache \
	caddy \
	curl \
	libcap \
	openssh-client \
	php81-curl \
	php81-fpm \
	php81-gettext \
	php81-iconv \
	php81-intl \
	php81-mbstring \
	php81-mysqli \
	php81-opcache \
	php81-openssl \
	php81-pdo_mysql \
	php81-pdo_odbc \
	php81-pdo_pgsql \
	php81-pdo_sqlite \
	php81-pecl-apcu \
	php81-pecl-memcache \
	php81-pecl-redis \
	php81-pecl-uploadprogress \
	php81-pecl-yaml \
	php81-pgsql \
	php81-session \
	php81-simplexml \
	php81-sodium \
	php81-sqlite3 \
	php81-xml \
	supervisor \
	tzdata

EXPOSE 80
VOLUME /config
VOLUME /srv

COPY Caddyfile supervisord.conf index.php /tmp/
RUN mkdir /config && mv /tmp/Caddyfile /config/Caddyfile && \
	mv /tmp/supervisord.conf /config/supervisord.conf && \
	mv /tmp/index.php /srv/index.php

RUN addgroup --gid ${LE_APP_GID} le_app && \
	adduser -D -S -s /sbin/nologin -G le_app --uid ${LE_APP_UID} le_app && \
	setcap cap_net_bind_service=+ep `readlink -f /usr/sbin/caddy` && \
	chown le_app:le_app /srv && \
	touch /run/supervisord.pid && \
	chown le_app:le_app /run/supervisord.pid /var/log/php81

USER le_app

CMD ["/usr/bin/supervisord", "-c", "/config/supervisord.conf"]
