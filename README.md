# Nginx SSL Proxy

This repostory uses [nginx-proxy][nginx-proxy] and
[nginx-proxy-letsencrypt][nginx-proxy-letsencrypt] docker containers.

[nginx-proxy]: https://github.com/jwilder/nginx-proxy
[nginx-proxy-letsencrypt]: https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion

## Description

Using this container you can easily publish your application (inside docker)
with SSL certificates signed by [Let's Encrypt](https://letsencrypt.org/).

## Usage

### Start Containers

Start containers with: `docker-compose up -d`

### Prepare Application

#### Environment

In your application's container define environment variables:

 * `VIRTUAL_HOST` (hostname used to resolve your application's location),
 * `VIRTUAL_PORT` (optional, used if your application's port differs from 80) and
 * `LETSENCRYPT_HOST` (hostname for certificate signing)

#### Network

Add your container to the external network with name `proxy`.

If you use docker-compose, add this to the end of compose file:

```
networks:
  proxy:
    external:
      name: "proxy"
```

And in the application's service:

```
networks:
  - "proxy"
```

If you use pure docker, then simply run:

```bash
docker network connect proxy <application_container>
```

Replace `<application_container>` with your application's container name
