## Remove default database servers from Forge instance
Tested on Ubuntu 16 - Homestead and Forge

Notes:

* MongoDB removal is commented-out as it's not installed by default for new Forge instances.

``` shell
###########################################################################
#
# Remove default database servers from Forge instance
# Tested on Ubuntu 16 - Homestead and Forge
#
# Notes:
# - MongoDB removal is commented-out as it's not installed by default for
#   new Forge instances.
#
###########################################################################

# remove MySQL
service mysql stop
killall -9 mysql
killall -9 mysqld
apt-get -y remove --purge mysql-server mysql-client mysql-common
apt-get -y purge mysql-server-core-5.5
apt-get -y purge mysql-client-core-5.5
apt-get -y purge --auto-remove mysql\*
apt-get -y autoremove
apt-get -y autoclean
deluser mysql
groupdel mysql
rm -rf /var/lib/mysql
rm -rf /var/log/mysql
rm -rf /etc/mysql

# remove PostgreSQL
service postgresql stop
killall -9 postgresql
apt-get -y purge --auto-remove postgresql\*
apt-get -y autoremove
apt-get -y autoclean
deluser postgresql
deluser postgres
groupdel postgresql
groupdel postgres
rm -rf /var/lib/postgresql
rm -rf /var/log/postgresql
rm -rf /etc/postgresql

# remove Redis
service redis-server stop
killall -9 redis-server
apt-get purge --auto-remove redis-server -y
apt-get -y purge --auto-remove redis\*
apt-get -y autoremove
apt-get -y autoclean
deluser redis-server
deluser redis
groupdel redis-server
groupdel redis
rm -rf /var/lib/redis
rm -rf /var/log/redis
rm -rf /etc/redis

# remove MongoDB
#sudo apt-get purge mongodb mongodb-clients mongodb-server mongodb-dev
#sudo apt-get purge mongodb-10gen
#sudo apt-get autoremove
```
