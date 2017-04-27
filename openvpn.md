# OpenVPN

> VPN for smart people.

## Install and Configure on FreeBSD 11

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

### Install OpenVPN

```bash
cd /usr/ports/security/openvpn
make install clean
```

### Make it Start Automatically on Boot

```bash
sysrc openvpn_enable="YES"
sysrc openvpn_config="/usr/local/etc/openvpn/server.conf"
```

### Create Server Configuration

```bash
mkdir /usr/local/etc/openvpn
cp /usr/local/share/examples/openvpn/sample-config-files/server.conf /usr/local/etc/openvpn/server.conf
```

### Generate Server Certificates and Keys

```bash
cp -r /usr/local/share/easy-rsa /usr/local/etc/openvpn/easy-rsa
cd /usr/local/etc/openvpn/easy-rsa
vi vars
./easyrsa.real init-pki
./easyrsa.real gen-dh
./easyrsa.real build-ca
./easyrsa.real build-server-full server
```

### Copy the Key Files and Certificates

```bash
cp /usr/local/etc/openvpn/easy-rsa/pki/dh.pem /usr/local/etc/openvpn/dh2048.pem
cp /usr/local/etc/openvpn/easy-rsa/pki/ca.crt /usr/local/etc/openvpn
cp /usr/local/etc/openvpn/easy-rsa/pki/private/server.key /usr/local/etc/openvpn
cp /usr/local/etc/openvpn/easy-rsa/pki/issued/server.crt /usr/local/etc/openvpn
```
