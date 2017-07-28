# FreeBSD Cheatsheet
> The handbook is great, but this is the short one.

## Table of Contents

- [Boot](#boot)
- [File Systems](#file-systems)
- [Jails](#jails)
- [Kernel](#kernel)
- [Networking](#networking)
- [Permissions](#permissions)
- [pkgng](#pkgng)
- [Software](#software)
- [SSH](#ssh)
- [Time](#time)
- [Updates](#updates)
- [ZFS](#zfs)

## Boot

### Reduce Boot-Time Delay
```
# /boot/loader.conf
autoboot_delay="3"
```

## File Systems

### Mount Linux EXT4 in LVM2
```bash
kldload /boot/kernel/geom_linux_lvm.ko
pkg install fusefs-ext4fuse
ext4fuse /dev/linux_lvm/volumegroup-logicalvolume /mnt
```


## Jails

### Completely Remove Jail Folders
```bash
chflags -R noschg /usr/jails && \
rm -rf /usr/jails
```


## Kernel

### Install Kernel and System Sources
```bash
svnlite checkout https://svn.freebsd.org/base/release/11.0.1 /usr/src
```


## Networking

### Prevent resolv.conf from Being Overwritten
```bash
chflags schg /etc/resolv.conf
```

### Restart Network Service over SSH
```bash
/etc/rc.d/netif restart && /etc/rc.d/routing restart
```

## Permissions

### Make file undeleteable, even by root
```bash
## Enable
chflags schg /path/to/file

## Disable
chflags noschg /path/to/file
```


## pkgng

### Fix Corrupt SQLite Database
Fixes "sqlite error while executing INSERT OR ROLLBACK INTO pkg_search".
```bash
pkg info -ao > pkglist.txt
rm /var/db/pkg/local.sqlite
pkg update -f
pkg install `cat pkglist.txt`
```


## Software

### Install Python with pip
```bash
pkg install python && \
python -m ensurepip
```


## SSH

### Create secure SSH key
```bash
ssh-keygen -o -a 100 -t ed25519
```


## Time

### Force Update Date and Time
```bash
service ntpd stop
ntpd -q -g
service ntpd start
```

## Updates

### Install portmaster
```bash
cd /usr/ports/ports-mgmt/portmaster && \
make install clean
```

### Install FreeBSD ports collection
```bash
portsnap fetch extract
```

### Upgrade FreeBSD ports collection
```bash
portsnap fetch update
```

### Fetch binary updates
```bash
freebsd-update fetch install
```

### Update FreeBSD from source
```bash
svn update /usr/src
# check /usr/src/UPDATING for manual steps
cd /usr/src
make -j4 buildworld
make -j4 kernel KERNCONF=GENERIC
shutdown -r now
cd /usr/src
make installworld
mergemaster -Ui
shutdown -r now
```

## ZFS

### Mount Pool with Different Root
Useful for untrusted pools or ones that mount to system directories.
```bash
zpool import -f -R /mnt pool
```

### Rescue ZFS-on-Root system
This comes in handy on `unable to remount devfs under dev` errors, for example. Reboot machine from USB/CD/network image. Select "Live System", then:
```bash
mkdir /tmp/mnt
zpool import -f -R /tmp/mnt zroot
zfs mount zroot/ROOT/default
chroot /tmp/mnt
...make changes...
exit
zpool export zroot
reboot
```
