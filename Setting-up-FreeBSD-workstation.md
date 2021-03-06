## Installation


### System

- Prepare the Installation Media (CD or USB memory stick)
- Boot from Installation Media and choose to Install the OS
- Uncheck all optional system components when prompted
- Choose manual partitioning and make sure to have following structure (assuming that size of free space is 16Gb):
    - Type: "freebsd", Size: "16Gb", Mountpoint: "", Primary partition
        - Type: "freebsd-ufs", Size: "14Gb", Mountpoint: "/", Logical partition
        - Type: "freebsd-swap", Size: "2Gb", Mountpoint: "", Logical partition
- Check sshd in system configuration menu
- Add user with defaults plus add them to group "wheel"


### MBR and FreeBSD Boot Manager

- Choose to stay in the shell or boot from Installation Media's and enter it's shell
- Run `sysctl kern.geom.debugflags=16` to be able changing the boot partition (not required if booted from Installation Media)
- Launch `sysinstall`, enter **Configure** section, launch **Fdisk** utility, set FreeBSD Primary partition as **Active** by pressing `s` keyword when it is selected, exit and choose FreeBSD Boot Manager to be installed in MBR
- Reboot and check that FreeBSD Boot Manager provides menu with all existing Operating Systems.
- In order to customize FreeBSD Boot Manager and remove some unwanted menu items refer to [boot0cfg](http://www.freebsd.org/cgi/man.cgi?query=boot0cfg) tool.

Here is a small tip on removing menu items. Assuming you have this menu:

  - F1 FreeBSD
  - F2 Windows
  - F3 ?

and you would like to remove the third one (looks like it's a FAT32 partition without any OS for file sharing between FreeBSD and Windows) you would run (replace `/dev/ada0` with your drive):

```
boot0cfg -m 0x3 /dev/ada0
```

0x3 is a hexadecimal of decimal 3, while 3 is a sum of integers that represent each active item. Each item's integer is previous item's integer multiplied by 2, so:

  - F1 = 1
  - F2 = 2
  - F3 = 4
  - etc.



## Post-installation


### Patch and update system

- Log in with root user
- Run `freebsd-update fetch install` - to install the latest OS patches
- Run `portsnap fetch extract` - to download and extract the ports tree (should be done only once)
- Run `portsnap fetch update` - to update the ports tree (repeat this step frequently)


### Build Kernel

- `cd /usr/src/sys/i386/conf`
- `mkdir /root/kernels`
- `cp GENERIC /root/kernels/WORKSTATION` or use [this template](https://gist.github.com/4032674) (check compatibility first)
- `ln -s /root/kernels/WORKSTATION`
- edit `/root/kernels/WORKSTATION` accordingly
- `cd /usr/src`
- `make buildkernel KERNCONF=WORKSTATION`
- `make installkernel KERNCONF=WORKSTATION`


### System settings

- In order to clean `/tmp` contents on boot, add following to `/etc/rc.conf`:
```
clear_tmp_enable="YES"
```
- Change boot menu ASCII logo `touch /boot/loader.conf` and add (see `/boot/beastie.4th` for available values):
```
loader_logo="beastie"
```
- Change welcome message for every user login in `/etc/motd`, for example:
```
cd /usr/ports/misc/figlet && make install distclean
figlet w00t
           ___   ___  _
__      __/ _ \ / _ \| |_
\ \ /\ / / | | | | | | __|
 \ V  V /| |_| | |_| | |_
  \_/\_/  \___/ \___/ \__|
```

### UTF-8

- Check current locale by running `locale`
- To enable UTF-8 for specific user add 2 lines to **me** block in **~/.login_conf**, like so (replace **en_US** with any available locale that is listed in `locale -a | grep UTF-8`):
```
me:\
   ...
   :charset=UTF-8:\
   :lang=en_US.UTF-8:
```
- To enable UTF-8 globally, add same 2 lines to **default** block in **/etc/login.conf** and run `cap_mkdb /etc/login.conf`
- Exit all active sessions and after login verify that new settings were applied by running `locale`


### Set mounts

Assuming you have, for example FAT32 partition to share files between Windows and FreeBSD

- Create `/mnt/shared` where we will mount our partition
- Run `fdisk` and find desired partition number (let's say it's **3**)
- Edit `/etc/fstab` and add following line:
```
/dev/ada0s3     /mnt/shared     msdosfs rw      0       0
```
- After reboot you should be able to Read/Write to the contents of /mnt/shared and access it from other OS on same machine


### SSH Logging

- Create file for logs `touch /var/log/sshd.log`
- Add following to `/etc/syslog.conf`:
```
!sshd
*.*                                             /var/log/sshd.log
```
- Make sure to have these lines in `/etc/ssh/sshd_config` (adjust **LogLevel** accordingly):
```
SyslogFacility AUTH
LogLevel DEBUG3
```


### Install Multi-User Dev Tools

- **IDE** `cd /usr/ports/editors/vim && make install clean`
- **Version Control System** `cd /usr/ports/devel/git && make install clean`
- **Shell** `cd /usr/ports/shells/zsh && make install clean`
- **Terminal Multiplexer** `cd /usr/ports/sysutils/tmux && make install clean`
- **Headless Webkit** `cd /usr/ports/lang/phantomjs && make install clean`
- **NodeJS** `cd /usr/ports/www/node && make install clean`
- **Npm** `cd /usr/ports/www/npm && make install clean`
- **libyaml** `cd /usr/ports/textproc/libyaml && make install clean` - required for ruby
- **optipng** `cd /usr/ports/graphics/optipng && make install clean`
- Make sure you have **jpegtran** installed as well
- **Yeoman** `npm install -g yeoman` - install this one after single-user installations are finished
- **Google Chrome** `cd /usr/ports/www/chromium && make install clean` - this will take some time, but it worth it

### Install Single-User Dev Tools

- Install **RVM** `\curl -L https://get.rvm.io | bash -s stable`, `source ~/.rvm/scripts/rvm`
- Make sure you have following in your shell's RC file (.bashrc, .zshrc or any other):
```
[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm" # This loads RVM into a shell session.  
```
- Install **Ruby** `rvm install 1.9.3`
- **Compass** `gem install compass`
- **Ruby On Rails** `gem install rails`

### Misc utilities & stuff (install according to need)

- Download nice system dump [script](https://github.com/KittyKatt/screenFetch) to **~/bin** or install **bsdinfo** `cd /usr/ports/sysutils/bsdinfo && make install clean`
- **htop** (system monitor) `cd /usr/ports/sysutils/htop && make install clean`
- **iftop** (network monitor) `cd /usr/ports/net-mgmt/iftop && make install clean`
- **mpg321** (Audio playback) `cd /usr/ports/audio/mpg321 && make install clean`
- **cplay** (Music CLI manager) `cd /usr/ports/audio/cplay && make install clean`
- **eyeD3** (read & edit MP3 ID3 tags) `easy_install eyeD3` Requires Python
- **Gnupg** (Encryption & Signing) `cd /usr/ports/security/gnupg && make install clean` (mark **Pinentry** checkbox)
- **tree** (list dirs contents as a tree) `cd /usr/ports/sysutils/tree && make install clean`
- **wget** (downloader) `cd /usr/ports/ftp/wget && make install clean`
- **sudo** (privileges tool) `cd /usr/ports/security/sudo && make install clean`
- Install CLI [dotfiles](https://github.com/sergeylukin/dotfiles) bundle

## GUI


### X Window System

- Install Xorg `cd /usr/ports/x11/xorg && make install clean` (X11 FreeBSD implementation)
- Add following lines to your **/etc/rc.conf**:
```
# Xorg
hald_enable="YES"
dbus_enable="YES"
```
- Build initial configuration file `Xorg -configure`
- Modify **/root/xorg.conf.new** or use [this template](https://gist.github.com/4039008) (check compatibility)
- Test `Xorg -config xorg.conf.new -retro`
- Deploy `mv xorg.conf.new /etc/X11/xorg.conf`
- You can change Console's Video Mode. To see all available video modes run `vidcontrol -i mode`. Assuming you picked mode **280**, test it with `vidcontrol MODE_280` and if it works fine add following to **/etc/rc.conf**:
```
# Console Video Mode
allscreens_flags="MODE_280"
```


### Desktop Environment

- Install **Xfce** `cd /usr/ports/x11-wm/xfce4 && make install clean`
- Set **Xfce** by default `echo "/usr/local/bin/startxfce4" > ~/.xinitrc` for current user only or `echo "/usr/local/bin/startxfce4" > /usr/local/lib/X11/xinit/xinitrc` for all users (run `find / -name xinitrc` to find correct path for global xinitrc file)



### Themes & Icons

- Download themes into **~/.themes** and select them in **Settings** -> **Window Manager** and **Settings** -> **Appearance** (highly recommend theme called **Victory (Strikes Again)**)
- Download icons into **~/.icons** and select them in **Settings** -> **Appearance** -> **Icons** (highly recommend [this icons pack](http://newhoa.deviantart.com/art/Victory-Icon-Collection-188206119))

OR

- Install [this pre-configured bundle](https://github.com/sergeylukin/dotfiles-xfce)


### Install Utilities

- **Opera** (Web browser) download latest version from [opera.com](http://opera.com), unpack and run `./install` script
- **xClip** (Xorg Buffer) `cd /usr/ports/x11/xclip && make install clean`
- **feh** (image viewer) `cd /usr/ports/graphics/feh && make install clean`
- **MPlayer** (Video playback) `cd /usr/ports/multimedia/mplayer && make install clean`
- **ffmpg** (Video converter) `cd /usr/ports/multimedia/ffmpeg && make install clean`