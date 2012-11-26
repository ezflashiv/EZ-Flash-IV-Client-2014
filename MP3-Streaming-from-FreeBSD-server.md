### Streaming Server (Icecast2)

- Install `cd /usr/ports/audio/icecast2 && make install clean`

- Start service on system boot:
```
echo "# Icecast2 streaming Server" >> /etc/rc.conf
echo "icecast_enable=YES" >> /etc/rc.conf
```

- Add Group and User with home directory to run the server and manage streams
```
pw groupadd icecast && pw useradd icecast -g icecast -m
```

- Create required directories and files:
```
mkdir -p /var/log/icecast
touch /var/log/icecast/access.log
touch /var/log/icecast/error.log
chown -R icecast:icecast /var/log/icecast
```

- Copy sample configuration file
```
cd /usr/local/etc && cp icecast.xml.sample icecast.xml
```

- Edit configuration file `vim /usr/local/etc/icecast.xml`:

    - Change values of `<admin-password>`, `<source-password>` and `<relay-password>`
    - In `<listen-socket>` group specify *IP* and *PORT* you want to stream from
    - In `<security>` group set both `<user>` and `<group>` to **icecast**
    - Set `<logdir>` to `/var/log/icecast`
    - Make sure all files paths exist and are correct - **!important**


- Start daemon `/usr/local/etc/rc.d/icecast2 start`

- Verify that Icecast2 is working by browsing to `http://IP:PORT`



### Install Source client for broadcasting (ices0)

- Install `cd /usr/ports/audio/ices0 && make install clean` - Select all options to enjoy the full stack of possibilities

- Copy sample configuration file:
```
cd /usr/local/etc && cp ices.conf.dist ices.conf
```

- Start service on system boot:
```
echo "# Ices0 - mp3 streaming" >> /etc/rc.conf
echo "ices0_enable=YES" >> /etc/rc.conf
```

- Edit configuration file `vim /usr/local/etc/ices.conf`:
    - In `<Server>` specify credentials of **Icecast2** server (including `<source-password>` as the value of `<Password>`)
    - In `<Type>` field type `python` in order to use Python script to manage streaming flow

- Copy sample Python script
```
cd /usr/local/etc/modules && cp ices.py.dist ices.py
```

- Edit Python script according to what you need - full freedom of fantasy. As a very starting point you can play randomly chosen tracks from `/home/icecast/music/` directory. For that edit `/usr/local/etc/modules/ices.py` like so:
```
from string import *
import sys, os, random
...
def ices_get_next ():
          return "/home/icecast/music/" + random.choice(os.listdir("/home/icecast/music/"))
...
```

### Tips

- In order to play next track immediately, first find out *ices0* PID: `ps aux | grep ices0` and send `SIGUSR1` signal to it:
```
kill -USR1 PID
```