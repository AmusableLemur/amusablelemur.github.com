+++
title = "Homelab Part 3: Domains"
date = "2024-03-17T10:00:00+02:00"
type = "post"
+++

The next part in setting things up is getting domains sorted. Since I have everything on the same IP address I created a wildcard subdomain pointing to my homelab. This way I can add any names without having to update the nameserver all the time.

## Caddy

Normally I would use nginx as a reverse proxy but Caddy has been up and coming and I was a bit excited to see how it would work. Getting it set up was incredibly simple.

I created a really simple stack for Caddy like the following. What is really nice here is I can have a Caddyfile defined somewhere I can edit it easily and mount it in.

````docker-compose
services:
  caddy:
    image: caddy:2.7
    container_name: caddy
    restart: unless-stopped
    networks:
      - proxy
    ports:
      - "80:80"
      - "443:443"
      - "443:443/udp"
    volumes:
      - /home/rasmus/Caddyfile:/etc/caddy/Caddyfile

networks:
  proxy:
    external: true
    name: proxy
````

This is also the only service stack with exposed ports, as all incoming traffic will pass through this proxy. This is done through a named network that I can reuse in other stacks to allow Caddy to reach those services as well and forward the traffic.

Adding a service, like Authelia for example, is incredibly simple compared to Apache2 or nginx. A simple block in the Caddyfile is enough. No need to expose the ports in Authelia either if I add the `proxy` network to that stack also.

````Caddyfile
auth.rasmuslarsson.se {
  reverse_proxy authelia:9091
}
````

## Forward auth

In addition to adding support for domains and acting as a reverse proxy Caddy supports [forward authentication](https://caddyserver.com/docs/caddyfile/directives/forward_auth). This is useful for protecting services that do not support OAuth or LDAP for authentication.

I can add the following to any service definition to get forward authentication working. The headers will also include information about the authenticated user.

````Caddyfile
  forward_auth authelia:9091 {
    method GET
    uri /api/verify?rd=https://auth.rasmuslarsson.se
    header_up X-Forwarded-Method {method}
    header_up X-Forwarded-Uri {uri}
    copy_headers Remote-User Remote-Groups Remote-Name Remote-Email
  }
````
