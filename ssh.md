# SSH Cheatsheet

> The secure shell.

## Table of Contents

- [SSH Configuration](#ssh-configuration)

## SSH Configuration

### Multiple SSH Hops
```
# ~/.ssh/config

Host bastion
  Hostname bastion.domain.com
  User bastion-user

Host server
  Hostname server.local.lan
  User server-user
  ProxyCommand ssh bastion -W %h:%p
```
