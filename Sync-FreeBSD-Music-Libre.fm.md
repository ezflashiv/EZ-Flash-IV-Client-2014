## Using CPlay

- Install Mpg321 (audio playback) `cd /usr/ports/audio/mpg321 && make install clean`
- Install Cplay (music front-end) `cd /usr/ports/audio/cplay && make install clean`
- Verify you Python version (installed if you don't have one), download according *.egg file (for example **setuptools-0.6c11-py2.7.egg** in my case) from [http://pypi.python.org/pypi/setuptools#files](http://pypi.python.org/pypi/setuptools#files) and run as *root* `sh setuptools-0.6c11-py2.7.egg`
- Download [scrobbler](http://sourceforge.net/projects/scrobbler/)
- Apply this [patch](http://sourceforge.net/tracker/?func=detail&aid=2789702&group_id=207796&atid=1003125)
- CD to folder with downloaded scrobbler and execute `easy_install .`
- Paste contents of [this file](https://github.com/SebastianZaha/cplay_scrobbler/blob/master/cplay_scrobbler.py) to `~/.cplayrc` and modify credentials accordingly. Also change this line:
```
scrobbler.login(USERNAME, PASSWORD, ('cpl', '1.0'))
```
to
```
scrobbler.login(USERNAME, PASSWORD, ('cpl', '1.0'), 'http://turtle.libre.fm/')
```
- Now when playing music with CPLay your libre.fm account will track that


## MOC

I would not recommend this method:) After I set up CPLay I unistalled MOC and all described in this section.

- Install MOC `cd /usr/ports/audio/moc && make install clean`
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