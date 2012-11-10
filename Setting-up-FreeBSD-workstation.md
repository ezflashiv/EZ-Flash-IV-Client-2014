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


### Install Dev Tools

- **IDE** `cd /usr/ports/editors/vim && make install clean`
- **Version Control System** `cd /usr/ports/devel/git && make install clean`
- **Shell** `cd /usr/ports/shells/zsh && make install clean`
- **Terminal Multiplexer** `cd /usr/ports/sysutils/tmux && make install clean`


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


### Install Utilities

- **Opera** download latest version from [opera.com](http://opera.com), unpack and run `./install` script
- **xClip** `cd /usr/ports/x11/xclip && make install clean`