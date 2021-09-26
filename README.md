# UPnP Service

## Purpose

Add an additional tool to the toolkit of avid homelabbers or individuals who might not have direct access to port forward services on their router. Networks that support [UPnP](https://en.wikipedia.org/wiki/Universal_Plug_and_Play) will be able to expose internal services to the WAN with little effort. This project was motivated by Google WiFi not supporting port forwarding to an ARP based Virtual IP (VIP). Trying to achieve High Availability without the ability to forward to a shared VIP proves to make for a lacking homelab.

## Pulling the Container

[ghcr](https://github.com/ProjectInitiative/upnp-service/pkgs/container/upnp-service)

[Docker Hub](https://hub.docker.com/repository/docker/projectinitiative/upnp-service)

```bash
docker pull projectinitiative/upnp-service:latest
# OR
docker pull ghcr.io/projectinitiative/upnp-service:latest
```

## Usage

All settings for running the container live in the `upnp.json` file (see next section). When running the container, the `host` network needs to be attached. This is achieved with `--network host` for the `docker` command, or `network_mode: host` in compose files.

## Config

The config JSON lives in `/etc/upnp-service/upnp.json`. This file will need to be mounted or edited in the container. Here is a sample of the data required to run properly:

```JSON
{
    "apps":
    [
        {
            "app_name": "app1",
            "redirections": [
                ["801", "TCP"],
                ["80801","80801","TCP"],
                ["80801","80801","UDP"]
            ]
        },
        {
            "app_name": "app2",
            "redirections": [
                ["4333","TCP"],
                ["4332","4334","TCP"]
            ]
        }
    ]
}

```

## Building from Source

```bash
cd $PROJ_DIR
docker build -t $TAG -f $PROJ_DIR/docker-image/Dockerfile $PROJ_DIR/docker-image
```

## Additional Info

Original credit and inspiration to [ofepk's Stack Overflow answer](https://stackoverflow.com/a/54081861) detailing a basic UPnP service docker container.