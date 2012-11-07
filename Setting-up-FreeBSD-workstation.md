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

### Post-installation

- Log in with root user
- Run `freebsd-update fetch install` - to install the latest OS patches
- Run `portsnap fetch extract` - to download and extract the ports tree