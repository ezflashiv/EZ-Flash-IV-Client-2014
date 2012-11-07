### Installation

- Prepare the Installation Media (CD or USB memory stick)
- Boot from Installation Media and choose to Install the OS
- Uncheck all optional system components when prompted
- Choose manual partitioning and make sure to have following structure (assuming that size of free space is 16Gb):
    - Type: "freebsd", Size: "16Gb", Mountpoint: "", Primary partition
        - Type: "freebsd-ufs", Size: "14Gb", Mountpoint: "/", Logical partition
        - Type: "freebsd-swap", Size: "2Gb", Mountpoint: "", Logical partition
- Check sshd in system configuration menu
- Add user with defaults plus add them to group "wheel"
- Run `sysctl kern.geom.debugflags=16` to be able changing the boot partition (only required if applying partition changes on drive you booted from)
- Launch `sysinstall`, enter **Configure** section, launch **Fdisk** utility, set FreeBSD Primary partition as **Active** by pressing `s` keyword when it is selected, exit and choose FreeBSD Boot Manager to be installed in MBR

### Post-installation

- Log in with root user
- Run `freebsd-update fetch install` - to install the latest OS patches
- Run `portsnap fetch extract` - to download and extract the ports tree (should be done only once)
- Run `portsnap fetch update` - to update the ports tree (repeat this step frequently)