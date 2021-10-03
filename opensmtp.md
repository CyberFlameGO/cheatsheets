# OpenSMTP Cheatsheet

> When you want email to just work.

## Table of Contents

- [Queue](#queue)

## Queue

### Show
If the queue is empty, this will output nothing.
```
doas smtpctl show queue
1de69818e6a83342|local|mta|auth|so@tld|dest@tld|dest@tld|1540362112|1540362112|0|2|pending|406|No MX found for domain
```

### Schedule
```
doas smtpctl schedule 1de69818e6a83342
```
```
doas smtpctl schedule all
```
