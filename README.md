# UPnP Server

## Purpose

Add an addional tool to the toolkit of avid homelabbers or individuals who might not have direct access to port forward services on their router. Networks that support [UPnP](https://en.wikipedia.org/wiki/Universal_Plug_and_Play) will be able to expose internal services to the WAN with little effort. This project was motivated by Google WiFi not supporting port forwarding to an ARP based Virtual IP (VIP). Trying to achieve High Availability without the ability to forward to a shared VIP proves to make for a lacking homelab.


## Usage

The config JSON lives in `/etc/upnp-server/upnp.json`. This file will need to be mounted or edited in the container. Here is a sample of the data required to run properly:

```JSON
{
    "apps":
    [
        {
            "app_name": "app1",
            "port": "80",
            "protocols": ["TCP,UDP"]
        },
        {
            "app_name": "app2",
            "port": "8080",
            "protocols": ["UDP"]
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

Original credit and inspiration to [ofepk's Stack Overflow answer](https://stackoverflow.com/a/54081861) detailing a basic UPnP server docker container.