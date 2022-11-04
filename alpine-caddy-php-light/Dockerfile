ARG ALPINE_VERSION=3.16
FROM gjvnq/alpine-caddy:${ALPINE_VERSION}

# This list mostly comes from MediaWiki, Wordpress and Drupal
RUN apk add --no-cache \
	php81-curl \
	php81-fpm \
	php81-gettext \
	php81-iconv \
	php81-intl \
	php81-mbstring \
	php81-mysqli \
	php81-opcache \
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
	php81-xml

COPY Caddyfile supervisord.conf index.php /tmp/
RUN mv /tmp/Caddyfile /config/Caddyfile && \
	mv /tmp/supervisord.conf /config/supervisord.conf && \
	mv /tmp/index.php /data/index.php

RUN chown le_app:le_app /var/log/php81

USER le_app

CMD ["/usr/bin/supervisord", "-c", "/config/supervisord.conf"]
# TODO: add health-check