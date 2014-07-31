# Third-party software

### Installing required packages on first boot

- `pkg install zsh`
- `pkg install vim`
- `pkg install tmux`
- `pkg install git`
- `pkg install node npm`
- `pkg install bash`

#### Jasmine 
- `pkg install qt4-qmake`

### Routine that should be repeated from time to time

- `pkg autoremove` - to remove dependencies that are not in use any more
- `pkg upgrade` to update all previously installed packages to their latest versions
- `pkg audit -F` to address any vulnerabilities known for previosly installed software

### Add routine tasks

- Create file `/etc/periodic.conf` with following contents:

```bash
#!/bin/sh

# Automatically perform a daily back up of the package database
# See 5.4.7 in http://www.freebsd.org/doc/en/books/handbook/pkgng-intro.html
#
# Restore package database with `pkg backup -r /var/backups/pkgng.db`
#
daily_backup_pkgdb_enable="Yes"
daily_backup_pkgdb_dir="/var/backups"
```

### Configure

- Save [this file](https://gist.githubusercontent.com/sergeylukin/bdd66197a79ef07b2bc2/raw/824d388b633815ac24d9707f587c45a74b2890ad/.vimrc) as `/root/.vimrc` in order to have nicely configured Vim for root user

- `adduser` to add my own user

- `chpass <USERNAME>` to change anything regarding that user

- Set UTF-8 locale by following [this guide](https://github.com/sergeylukin/dotfiles/wiki/Setting-up-FreeBSD-workstation#utf-8)