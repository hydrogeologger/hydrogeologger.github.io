---
layout: post
title: installing wordpress on aliyun
---

# 1. ali yun install for wordpress 2018-09-05 10:35 
install required software

 {% highlight bash %}
apt-get install mysql-client mysql-server libapache2-mod-php7.0 php7.0-mysql
 {% endhighlight %}
libapache2-mod-php7.0 is important to be able to parse php file properly

 {% highlight bash %}
wget http://wordpress.org/latest.tar.gz
tar -xzvf latest.tar.gz 
mysql -u root -p

 {% endhighlight %}

 {% highlight bash %}
CREATE DATABASE wpdatabase;
CREATE USER wpuser@localhost;
SET PASSWORD FOR wpuser@localhost= PASSWORD("dbpassword");
GRANT ALL PRIVILEGES ON wpdatabase.* TO 
wpuser@localhost IDENTIFIED BY 'dbpassword';
FLUSH PRIVILEGES;
exit
 {% endhighlight %}
in the file wp-config.php

 {% highlight bash %}
// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define('DB_NAME', 'wpdatabase');

/** MySQL database username */
define('DB_USER', 'wpuser');

/** MySQL database password */
define('DB_PASSWORD', 'dbpassword');

 {% endhighlight %}

 {% highlight bash %}
 chown -R www-data:www-data /var/www/html
 find /var/www/html -type d -exec chmod 755 {} \;
 find /var/www/html -type f -exec chmod 644 {} \;
 {% endhighlight %}
above is important

NOTE

 the file address is /var/www/html/    in debian stretch

chinese support is done by enable a plugin multiligual 
 
reference:

https://linuxconfig.org/how-to-install-wordpress-on-debian-9-stretch-linux

https://www.digitalocean.com/community/tutorials/how-to-install-wordpress-on-debian-7




# 2. the password for root in mysql is lost

https://stackoverflow.com/questions/41645309/mysql-error-access-denied-for-user-rootlocalhost

the etc location is /etc/mysql/my.cnf

add both 
[mysqld] 

skip-grant-tables 

now run 

mysql -u root -p


second, the 
