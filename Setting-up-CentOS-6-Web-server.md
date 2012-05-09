### System settings
* set locale to UTF-8. Add following to /etc/profile:
```
# set locale to UTF-8
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8
```

### Users
* useradd www
* useradd -G www developername

### Dev tools
* yum groupinstall "Development Tools"
* yum install man wget vim readline-devel mlocate mc

### Apache
* yum install httpd
* chkconfig --levels 235 httpd on
* chown www:www /var/www -R
* Set ServerName to 127.0.0.1:80 and NameVirtualHost to *:80 in /etc/httpd/conf/httpd.conf
* add Include virtuals/* to /etc/httpd/conf/httpd.conf
* Add Virtual hosts files in /etc/httpd/virtuals/
* Let others view logs: `chmod o+rx /var/log/httpd`

### Ruby

Install YAML (required):

* Download & extract latest version from http://pyyaml.org/download/libyaml/
* change directory to yaml's source
* ./configure --prefix=/usr/local
* make && make install

Install RUBY:

* cd /usr/local/src
* download & extract latest version from http://www.ruby-lang.org/en/downloads/
* change directory to ruby's source
* ./configure --prefix=/usr/local --enable-shared --disable-install-doc --with-opt-dir=/usr/local/lib
* make && make install

### Ruby Gems
* cd /usr/local/src
* download & extract latest version from http://rubygems.org/pages/download
* ruby setup.rb

### Gems
* gem install jekyll

### MySQL
* yum install mysql-server mysql
* chkconfig --levels 235 mysqld on
* mysql -u root
* Run `SELECT User, Host FROM mysql.user;`
* For every root found, run:
`
SET PASSWORD FOR 'root'@'%HOST%' = PASSWORD('new-password');
`

For example:

```
SET PASSWORD FOR 'root'@'localhost' = PASSWORD('new-password');

SET PASSWORD FOR 'root'@'myserver' = PASSWORD('new-password');

SET PASSWORD FOR 'root'@'127.0.0.1' = PASSWORD('new-password');
```
* For every empty user, run:
`
DROP USER ''@'%HOST%';
`

For example:

```
DROP USER ''@'localhost';

DROP USER ''@'myserver';
```

### PHP
* as described [here](http://benramsey.com/blog/2012/03/build-php-54-on-centos-62/)
* ..
* ./configure --prefix=/usr/local --with-apxs2=/usr/sbin/apxs --with-mysql --with-mysqli --with-pdo-mysql'
* make && make install
* ..
* add following to /etc/httpd/conf.d/php.conf:


```
# PHP Configuration for Apache
#
# Load the apache module
#
LoadModule php5_module modules/libphp5.so
#
# Cause the PHP interpreter handle files with a .php extension.
#
<Files *.php>
  SetOutputFilter PHP 
  SetInputFilter PHP 
  LimitRequestBody 9524288
</Files>
AddType application/x-httpd-php .php
AddType application/x-httpd-php-source .phps
#
# Add index.php to the list of files that will be served as directory
# indexes.
#
DirectoryIndex index.php
```

### PhpMyAdmin
* Download latest version from http://www.phpmyadmin.net
* unpack and change directory
* cp config.sample.inc.php config.inc.php
* In config.inc.php replace `localhost` to `127.0.0.1`
* Uncomment storage settings and run /examples/create_tables.sql to enable Visual Designer
* login via web interface


### Misc
* Disable SELinux: set SELINUX=disabled in /etc/selinux/config
(reboot to apply changes or run /usr/sbin/setenforce 0)
* Copy /usr/local/src/php/php.ini-dev /usr/local/lib/php.ini