## Installation

- Download [lastfmsubmitd](http://hg.dereckson.be/freebsd-ports/src/505be8423e97/audio/lastfmsubmitd?at=default) port to `/usr/ports/audio/lastfmsubmitd`
- Execute following script:
```
pw groupadd -n lastfm -g 212
pw useradd  -n lastfm -u 212 -c "liblastfmd daemon" -d /nonexistent -g lastfm -s /nonexistent
for d in /var/log /var/run /var/spool; do
  mkdir $d/lastfm
  chown lastfm:lastfm $d/lastfm
  chmod 775 $d/lastfm
done
fi
```
- Add records regarding `lastfm` group/user from `/etc/group` and `/etc/passwd` to `/usr/ports/GIDs` and `/usr/ports/UIDs` respectively.
- `cd /usr/ports/audio/lastfmsubmitd && make install clean`
- Create `/usr/local/etc/lastfmsubmitd.conf` file with following contents:
```
[server]
url = http://turtle.libre.fm
[account]
user: USERNAME
password: ********
```

- Add `lastfmsubmitd_enable="YES"` to `/etc/rc.conf`
- Run daemon `/usr/local/etc/rc.d/lastfmsubmitd start`
- Now any tracks played in MOC should be scrobbled to Libre.fm.