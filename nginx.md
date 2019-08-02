# Nginx Cheatsheet
> Can do it all — and does it.

## Table of Contents

- [SSL](#ssl)

## SSL

### Create a Snakeoil Certificate
Useful to configure a server config before getting a proper one, like Let's Encrypt.
```sh
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /usr/local/etc/ssl/snakeoil.key -out /usr/local/etc/ssl/snakeoil.crt
```
