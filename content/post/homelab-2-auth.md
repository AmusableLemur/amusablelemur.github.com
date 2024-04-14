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

![lldap interface](/static/lldap.png)

## Login page and OAuth with Authelia

WIP :-)
