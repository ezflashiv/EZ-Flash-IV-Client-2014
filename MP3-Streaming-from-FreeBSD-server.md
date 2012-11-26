### Streaming Server (Icecast2)

- Install `cd /usr/ports/audio/icecast2 && make install clean`

- Start service on system boot:
```
echo "# Icecast2 streaming Server" >> /etc/rc.conf
echo "icecast_enable=YES" >> /etc/rc.conf
```

- Add Group and User to run the server
```
pw groupadd icecast && pw useradd icecast -g icecast
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
    - In `<listen-socket>` group specify IP and Port you want to stream from
    - In `<security>` group set both `<user>` and `<group>` to **icecast**
    - Set `<logdir>` to `/var/log/icecast`
    - Make sure all files paths exist and are correct - **!important**


- Start daemon `/usr/local/etc/rc.d/icecast2 start`

- Test by browsing to `http://YOUR_IP:YOUR_PORT`



### Install Source client for broadcasting (Ices0)

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

- Edit Python script according to what you need - full freedom of fantazy. As a very starting point you can create a file `/tmp/next_song` with full path for a MP3 file and edit `/usr/local/etc/modules/ices.py` to read it's content every time before it changes the song:
```
...
def ices_get_next ():
    f = open('/tmp/next_song','r')
    song_path = f.read().strip()
    f.close()
    return song_path

...
```