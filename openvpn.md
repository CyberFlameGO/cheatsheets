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

### Set Firewall Rules

```
# /etc/pf.conf

### Internal Interface
if_int=bge0

### Client network
vpnclients = "10.8.0.0/24"

### OpenVPN Port
openvpnport = "{ 443 }"
icmptypes = "{ echoreq, unreach }"

set skip on lo

### Enable NAT for OpenVPN Clients
nat on $if_int inet from $vpnclients to any -> $if_int

block in

pass in on $if_int proto tcp from any to $if_int port $openvpnport
pass in on $if_int from any to any
pass in inet proto icmp all icmp-type $icmptypes
pass out quick
```

### Enable Firewall on Boot

```
# /etc/rc.conf

gateway_enable="YES"
pf_enable="YES"
pf_rules="/etc/pf.conf"
```

### Enable IP Forwarding

``` bash
sysctl net.inet.ip.forwarding=1
```

### Load Firewall Rules and Enable

```bash
pfctl -ef /etc/pf.conf
```

### Edit Configuration, Test and Start
```bash
ee /usr/local/etc/openvpn/server.conf
openvpn --config /usr/local/etc/openvpn/server.conf
service openvpn start
```
