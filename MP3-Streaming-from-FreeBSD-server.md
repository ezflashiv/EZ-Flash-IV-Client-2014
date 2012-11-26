### Setup

- Install **Icecast2**
```
cd /usr/ports/audio/icecast2 && make install clean
```

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
mkdir -p /usr/local/var/log/icecast
touch /usr/local/var/log/icecast/access.log
touch /usr/local/var/log/icecast/error.log
chown -R icecast:icecast /usr/local/var/log/icecast
```

- Copy example configuration file
```
cd /usr/local/etc && cp icecast.xml.sample icecast.xml
```

- Edit configuration file `vim /usr/local/etc/icecast.xml`:

    - Change values of `<admin-password>`, `<source-password>` and `<relay-password>`
    - In `<listen-socket>` group specify IP and Port you want to stream from
    - In `<security>` group set both `<user>` and `<group>` to **icecast**
    - Make sure all files paths exist and are correct - **!important**

- Start daemon `/usr/local/etc/rc.d/icecast2 start`
- Test by browsing to `http://YOUR_IP:YOUR_PORT`