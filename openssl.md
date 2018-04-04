# OpenSSL

> Security is a good thing.

## Create dhparam
```bash
openssl dhparam -out /etc/ssl/dhparam.pem
```

## Remove Passphrase from SSL Key
```bash
openssl rsa -in www.key -out new.key
```
