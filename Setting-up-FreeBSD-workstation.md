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