ARG ALPINE_VERSION=3.16
FROM gjvnq/alpine-base:${ALPINE_VERSION}

RUN apk add --no-cache caddy
EXPOSE 80

COPY Caddyfile /config/Caddyfile

RUN setcap cap_net_bind_service=+ep `readlink -f /usr/sbin/caddy`

USER le_app

CMD ["caddy", "run", "--config", "/config/Caddyfile"]
# TODO: add health-check