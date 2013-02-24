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