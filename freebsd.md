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

### Mount Samba Share
```bash
mount_smbfs -I 1.2.3.4 //username@server/share /path/to/local/mnt
```

### Mount Samba Share with Credentials
```
# ~/.nsmbrc
[SERVER:USERNAME]
password=password
```
```bash
mount_smbfs -N -I 1.2.3.4 //username@server/share /path/to/local/mnt
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

### Setup ccache
2 GB tmpfs
```bash
portmaster devel/ccache
mkdir /ram
echo 'none /ram tmpfs rw,size=2147483648 0 0' >> /etc/fstab
mount /ram
```

### Basic make.conf for Headless Servers
```
# ccache
WRKDIRPREFIX=/ram
CCACHE_DIR=/var/cache/ccache
WITH_CCACHE_BUILD=yes

# Build Optimizations
CPUTYPE?=native
OPTIONS_SET=OPTIMIZED_CFLAGS CPUFLAGS
BUILD_OPTIMIZED=YES

# Headless server options
OPTIONS_SET+=ICONV
OPTIONS_UNSET=CUPS DEBUG FONTCONFIG NLS X11
WITHOUT_MODULES=sound ntfs linux

# Disable sendmail
NO_SENDMAIL=true

# Fresh OpenSSL from Ports
DEFAULT_VERSIONS+=ssl=openssl
```

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

### Set timezone
```bash
ln -s /usr/share/zoneinfo/Asia/Calcutta /etc/localtime
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
For a new release:
```bash
mv /usr/src /usr/src.bak
svn checkout https://svn.freebsd.org/base/releng/11.1 /usr/src
```

Always:
```bash
svn update /usr/src
less /usr/src/UPDATING
cd /usr/src
make -j4 buildworld
make -j4 kernel
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

### Remount Read-Only Root ZFS Pool as Read-Write
```bash
zfs set readonly=off zroot
```
