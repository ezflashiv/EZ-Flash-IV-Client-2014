### Streaming Server (icecast2)

- Install `cd /usr/ports/audio/icecast2 && make install clean`

- Start service on system boot:
```
echo "# icecast2 streaming Server" >> /etc/rc.conf
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

- Verify that icecast2 is working by browsing to `http://IP:PORT`



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
    - In `<Server>` specify credentials of **icecast2** server (including `<source-password>` as the value of `<Password>` from icecast2 configuration file)
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

- Finally, launch your stream:
```
ices0
```

### Tips

- In order to play next track immediately, first find out *ices0* PID: `ps aux | grep ices0` and send `SIGUSR1` signal to it:
```
kill -USR1 PID
```

- In order to serve multiple streams you don't need to modify icecast2 configuration (unless you need to stream from different port). You need to create additional ices0 configuration file, probably separate Python (or Perl) script, and you can launch it with `ices0 -c /path/to/my/config/file`. From there you can listen to your new station.  
In order to keep things in structure I created `/home/icecast/stations` directory with sub-directories that contain configuration file for each station and a symlink to python script (for example for station `ices` I would do `ln -s /usr/local/etc/modules/ices.py /home/icecast/stations/ices/ices.py`). Additionally I modified `/usr/local/etc/rc.d/ices0` script to require configuration file from `/home/icecast/stations/ices/ices.conf`. Also I changed ownership of all those files to `icecast:icecast` so that all streaming thing could be managed by `icecast` user.

- I recommend enabling `<Reencode>` in ices0 if you are not sure whether you need it or not, setting [Bitrate](http://en.wikipedia.org/wiki/Bit_rate) to 96kb/s at least and [Samplerate](http://en.wikipedia.org/wiki/Sampling_rate) to 44100 (make sure it is multiple of 11025Hz to ensure the encoding is compatible with most media players)

- For decrease latency as much as possible (difference in time between when the source plays a clip and the listener hears a clip) I set `<burst-on-connect>` and `<burst-size>` to 0 in icecast2 configuration. If latency is not an issue though, I suggest increasing these values.