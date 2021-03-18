# OpenSSL Cheatsheet

> Security is a good thing. Web security in particular.

## Create Self-Signed Certificate
```bash
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365
```

## Create dhparam
```bash
openssl dhparam -out /usr/local/etc/ssl/dhparam.pem 4096
```

## Remove Passphrase from SSL Key
```bash
openssl rsa -in www.key -out new.key
```
