### Ports and Packages

Remove port

```
cd /usr/ports/path
make deinstall-all clean
```

Show port configuration files

```
make showconfig
```

Remove port configuration files (recursively)

```
make rmconfig-recursive
```

Check if port is installed

```
pkg_info | grep PACKAGE_NAME
```

### Archives

Extract `.ISO` image contents

```
mdconfig -a -t vnode -f myImg.iso # assuming you get "md0" in response
mount -t cd9660 /dev/md0 /mnt/tmp
```

Following command will delete created `md0` device

```
mdconfig -d -u 0
```

..alternatively you could utilize `tar` to do that I guess.