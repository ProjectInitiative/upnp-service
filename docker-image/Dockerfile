FROM alpine:latest

RUN apk update
RUN apk add --no-cache bash jq miniupnpc

RUN mkdir /scripts
WORKDIR /scripts
COPY update_upnp .
RUN chmod a+x ./update_upnp

# cron to update each UPnP entries every 10 minutes
RUN echo -e "*/10\t*\t*\t*\t*\tbash /scripts/update_upnp 8080 TCP" >> /etc/crontabs/root

CMD ["crond", "-f"]

# on start, open needed ports
ENTRYPOINT bash update_upnp 80 TCP && bash update_upnp 8080 TCP