# Nginx Cheatsheet

> Can do it all — and does it.

## Table of Contents

- [Configuration](#configuration)
- [SSL](#ssl)

## Configuration

### Prevent Crawlers from Indexing Certain Files
```
location ~ \.(m4v|oga|ogg|pdf)$ {
    try_files $uri $uri/;
    add_header X-Robots-Tag "noindex, nofollow, nosnippet, noarchive";
}
```

## SSL

### Create a Snakeoil Certificate
Useful to configure a server config before getting a proper one, like Let's Encrypt.
```sh
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /usr/local/etc/ssl/snakeoil.key -out /usr/local/etc/ssl/snakeoil.crt
```
