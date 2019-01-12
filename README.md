# centos7.3  apache2.4 mariadb10.3 mysql7.2 install 

```
https://www.rosehosting.com/blog/how-to-install-php-7-2-on-centos-7/
http://aeac.tistory.com/21 (굿★★★★★)

yum update
rpm -qa libjpeg* libpng* freetype* gd-* gcc gcc-c++ gdbm-devel libtermcap-devel
yum install libjpeg* libpng* freetype* gd-* gcc gcc-c++ gdbm-devel libtermcap-devel
yum install httpd
vi /etc/yum.repos.d/MariaDB.repo

# MariaDB 10.3 CentOS repository list - created 2019-01-10 05:39 UTC
# http://downloads.mariadb.org/mariadb/repositories/
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.3/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1

yum install MariaDB-server MariaDB-client

#https://webtatic.com/projects/yum-repository/
 
rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm

yum install php72w

yum install php72w-b* php72w-c* php72w-d* php72w-e* php72w-f* php72w-g* php72w-i* php72w-l*
yum install php72w-p* php72w-mysqlnd* php72w-o* php72w-p* php72w-r* php72w-s* php72w-t* php72w-x*
yum install php72w-mbstring.x86_64

yum search php72w

httpd -v
php -v
mysql -V



yum install iptables-services  ( https://stackoverflow.com/questions/24756240/how-can-i-use-iptables-on-centos-7 )

vi /etc/sysconfig/iptables

# sample configuration for iptables service
# you can edit this manually or use system-config-firewall
# please do not ask us to add additional ports/services to this default configuration
*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A INPUT -p tcp -m state --state NEW -m tcp --dport 22 -j ACCEPT
-A INPUT -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT
-A INPUT -p tcp -m state --state NEW -m tcp --dport 443 -j ACCEPT

-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A FORWARD -j REJECT --reject-with icmp-host-prohibited
COMMIT

service iptables restart

iptables -nL


systemctl enable httpd    (   systemctl disable httpd )

/etc/httpd/conf.d/php.conf 에서

 DirectoryIndex index.html index.php 
 AddType application/x-httpd-php .php .html .htm .inc


/etc/php.ini
 short_open_tag = On

systemctl start mariadb
systemctl enable mariadb


mysql_secure_installation

```
