# OpenVPN

> VPN for smart people.

## Install on FreeBSD 11

### Load Kernel Modules

Load into active session:
```bash
kldload if_tap
kldload if_tun
```

To load again on boot, add to `/boot/loader.conf`:
```conf
if_tap_load="YES"
if_tun_load="YES"
```
