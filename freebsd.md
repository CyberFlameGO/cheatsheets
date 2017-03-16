# FreeBSD Cheatsheet
> The handbook is great, but this is the short one.

## Table of Contents

- [File Systems](#file-systems)
- [Jails](#jails)
- [Kernel](#kernel)
- [Networking](#networking)
- [Software](#software)
- [Updates](#updates)
- [ZFS](#zfs)


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

### Install Kernel Sources
```bash
fetch ftp://ftp.freebsd.org/pub/FreeBSD/releases/amd64/10.3-RELEASE/src.txz
tar -C / -xvzf src.txz
```


## Networking

### Prevent resolv.conf from Being Overwritten
```bash
chflags schg /etc/resolv.conf
```


## Software

### Install Python with pip
```bash
pkg install python && \
python -m ensurepip
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
