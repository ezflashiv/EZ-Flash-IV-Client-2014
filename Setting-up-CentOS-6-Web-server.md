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

Install YAML (required):

* Download & extract latest version from http://pyyaml.org/download/libyaml/
* change directory to yaml's source
* /configure --prefix=/usr/local
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

### PHP
* as described [here](http://benramsey.com/blog/2012/03/build-php-54-on-centos-62/)