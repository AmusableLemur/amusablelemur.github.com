+++
title = "Homelab Part 2: Authentication with LDAP and OAuth"
date = "2024-03-10T10:00:00+02:00"
type = "post"
+++

An annoying part about hosting services myself is managing passwords and logins for everything. Every service is a new user account with a separate password for security. Giving someone else access to a couple of services means setting up the same amount of user accounts for that person.

The simple solution to this is centralized authentication. This is commonly solved with LDAP (Lightweight Directory Access Protocol) or with OAuth depending on the methods of authentication. There is also OpenID Connect (OIDC) which is an additional layer on top of OAuth which allows services to create users and access rights on the fly.

## User management with LLDAP (Light LDAP)

The LDAP implementation allows services to get user information from a centralized place. While this is possible to do also with OAuth with OIDC not all services support this. For this reason I set up LDAP with an OAuth provider in front. That way I only have to configure users once (in LDAP) but will have support for LDAP, OAuth, and OIDC.

Here I found [LLDAP](https://github.com/lldap/lldap) which made the whole process rather simple. So, with a new docker-compose stack in Portainer I added the following.

````docker-compose
services:
  lldap:
    image: lldap/lldap:stable
    container_name: lldap
    networks:
      - database_postgres
    ports:
      - "17170:17170" # For the web front-end
    volumes:
      - "lldap_data:/data"

networks:
  database_postgres:
    external: true
    name: database_postgres
````

This gives LLDAP access to the PostgreSQL database server I set up previously. The database and connection string is configured with environment variables as are additional secrets.

![lldap interface](/media/lldap.png)

## Login page and OAuth with Authelia

Many services do not support authenticating against LDAP directly but instead rely on OAuth and OIDC. There are multiple ways to solve this but [Authelia](https://www.authelia.com/) was simple and lightweight while still enough for my needs.

Configuration against LLDAP was super easy and well documented. The only catch I ran into here was that the session domain needs to match the TLD for sessions to persist properly on redirects. Without this I got caught in a redirect loop when trying to log in.

Even though Authelia is pretty lightweight the configuration options are extensive and takes some time to go through. There is a really nice list of [examples for integrations](https://www.authelia.com/integration/prologue/introduction/) to find supported services to set up.

````docker-compose
services:
  authelia:
    container_name: authelia
    image: docker.io/authelia/authelia:latest
    restart: unless-stopped
    volumes:
      - "authelia_config:/config"
      - "authelia_secrets:/secrets"
````

Another thing here is that since this connects to the LLDAP instance which is on the same stack there is no need for another network to be configured here for it to be reachable. However, the volumes are necessary to store configuration and secrets.

Adding a client i.e. integration is a little bit of a hassle as it requires a unique key for the authentication flow and requires manually editing the config file. Putting this secret in the config file also makes the configuration a bit more complex to version control.

The unique key, or secret, can be easily generated through Docker though which is nice.

````bash
docker run authelia/authelia:latest authelia crypto hash generate argon2 --random --random.length 64 --random.charset alphanumeric
`````
