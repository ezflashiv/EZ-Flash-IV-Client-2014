#### Desktop icons

Install tweaking tool:

```
yum install gnome-tweak-tool
```

Launch it:

```
gnome-tweak-tool
```

GUI tool will open up. Go to **Dektop** and enable **Have file manager handle the desktop**

Now anything added to `~/Desktop` will show up in Desktop. It's better to copy `*.desktop` items there.
Here is an example of placing some shortcuts:

```
cp /usr/share/applications/firefox.desktop ~/Desktop/
cp /usr/share/applications/skype.desktop ~/Desktop/
```

To add Shutdown icon on Desktop create `~/Desktop/Shutdown.desktop` with following contents:

```
Desktop Entry]
Name=Shutdown
Comment=Power off
Exec=/sbin/shutdown -h now
Icon=/usr/share/icons/hicolor/48x48/apps/abrt.png
Terminal=false
Type=Application
Encoding=UTF-8
Categories=Network;Application;
MimeType=x-scheme-handler/skype;
X-KDE-Protocols=skype
Name[en_US]=Shutdown
```

#### Startup applications/scripts

Open startup preferences GUI tool:

```
gnome-session-properties
```

Click `Add` to add any scripts that should be executed on startup.

#### Enabling third party repo with MP3 goodies:

Go to [rpmfusion](http://rpmfusion.org/Configuration) and follow setup instructions