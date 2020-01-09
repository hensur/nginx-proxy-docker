# Docker NGINX reverse proxy example

# Installation
## Setup ssl certs
Generate a self signed certificate or copy an existing one to `./ssl`

### Self Signed Generation
```
cd ssl
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 1365 -subj '/CN=HOSTNAME' -nodes
```
Replace HOSTNAME with the desired one, or just enter the IP Address of the server.

## Setup upstream containers
There are two server blocks in `nginx.conf`. To use different upstream servers, replace the server name and port in the `proxy_pass` directive of the `location / {` block.

The server name should be equal to the container name in `docker-compose.yml`.

## Startup
Before starting the compose stack, setup the docker network:
```
docker network create system_traefik
```

All containers inside of this network can be proxied.
