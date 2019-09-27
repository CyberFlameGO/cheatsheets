# Postfix Cheatsheet

> Concise email management.

## Table of Contents

- [Configuration Options](#configuration-options)
- [Spam Blocking](#spam-blocking)

## Configuration Options

### Message Size
This example limits to ~ 25 MB. Attachments are ~ 30% bigger than displayed.
```
# /etc/postfix/main.cf

message_size_limit = 25600000
```

## Spam Blocking

### Whitelisting
```
# /etc/postfix/rbl_override

1.2.3.4 OK
domain.tld OK
```

### RBL Blacklisting

```
# /etc/postfix/main.cf

[...]
smtpd_recipient_restrictions =
    reject_invalid_hostname,
    reject_unauth_pipelining,
    permit_mynetworks,
    permit_sasl_authenticated,
    reject_unauth_destination,
    check_client_access hash:/etc/postfix/rbl_override,
    reject_rbl_client multi.uribl.com,
    reject_rbl_client dsn.rfc-ignorant.org,
    reject_rbl_client dul.dnsbl.sorbs.net,
    reject_rbl_client list.dsbl.org,
    reject_rbl_client sbl-xbl.spamhaus.org,
    reject_rbl_client bl.spamcop.net,
    reject_rbl_client dnsbl.sorbs.net,
    reject_rbl_client cbl.abuseat.org,
    reject_rbl_client ix.dnsbl.manitu.net,
    reject_rbl_client combined.rbl.msrbl.net,
    reject_rbl_client rabl.nuclearelephant.com,
    permit
[...]
```

```bash
postmap /etc/postfix/rbl_override
service postfix restart
```
