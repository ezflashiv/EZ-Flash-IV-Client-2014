### Users
* useradd www
* useradd -G www developername

### Dev tools
* yum groupinstall "Development Tools"
* yum install man wget vim readline-devel

### Apache
* yum install httpd
* chkconfig --levels 235 httpd on
* chown www:www /var/www -R
* Set ServerName to 127.0.0.1:80 and NameVirtualHost to *:80 in /etc/httpd/conf/httpd.conf
* Add Virtual hosts files in /etc/httpd/conf.d/

### Ruby
* cd /usr/local/src
* Download latest version from http://www.ruby-lang.org/en/downloads/
* tar xvfz ruby*.tar.gz
* cd ruby*
* ./configure
* make && make install

### PHP
* as described [here](http://benramsey.com/blog/2012/03/build-php-54-on-centos-62/)