#TODO: reduce number of installed packages
ARG ALPINE_VERSION=3.16
FROM gjvnq/alpine-caddy:${ALPINE_VERSION}

# This list mostly comes from MediaWiki, Wordpress and Drupal
USER root
RUN apk add --no-cache \
	composer \
	git \
	imagemagick \
	openssh-client \
	php81-bcmath \
	php81-bz2 \
	php81-calendar \
	php81-ctype \
	php81-curl \
	php81-dba \
	php81-dom \
	php81-enchant \
	php81-exif \
	php81-fileinfo \
	php81-fpm \
	php81-ftp \
	php81-gd \
	php81-gettext \
	php81-gmp \
	php81-iconv \
	php81-imap \
	php81-intl \
	php81-ldap \
	php81-mbstring \
	php81-mysqli \
	php81-opcache \
	php81-openssl \
	php81-pcntl \
	php81-pdo_mysql \
	php81-pdo_odbc \
	php81-pdo_pgsql \
	php81-pdo_sqlite \
	php81-pear \
	php81-pecl-apcu \
	php81-pecl-imagick \
	php81-pecl-memcache \
	php81-pecl-memcached \
	php81-pecl-redis \
	php81-pecl-uploadprogress \
	php81-pecl-yaml \
	php81-pecl-zstd \
	php81-pgsql \
	php81-posix \
	php81-session \
	php81-simplexml \
	php81-sockets \
	php81-sodium \
	php81-sqlite3 \
	php81-tidy \
	php81-xml \
	php81-xmlreader \
	php81-xmlwriter \
	php81-zip

COPY Caddyfile supervisord.conf index.php /tmp/
RUN mv /tmp/Caddyfile /config/Caddyfile && \
	mv /tmp/supervisord.conf /config/supervisord.conf && \
	mv /tmp/index.php /data/index.php

RUN chown le_app:le_app /var/log/php81

USER le_app

CMD ["/usr/bin/supervisord", "-c", "/config/supervisord.conf"]
# TODO: add health-check