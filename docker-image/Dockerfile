FROM alpine:latest

RUN apk update
RUN apk add --no-cache bash jq miniupnpc

# create default settings file
RUN mkdir -p /etc/upnp-service
COPY upnp.json /etc/upnp-service


COPY entrypoint /usr/local/bin
COPY update_upnp /usr/local/bin
RUN chmod a+x /usr/local/bin/entrypoint
RUN chmod a+x /usr/local/bin/update_upnp

ENTRYPOINT [ "entrypoint" ]
