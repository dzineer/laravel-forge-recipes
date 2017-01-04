```
###########################################################################
#
# MongoDB server and php-mongo install
# Tested on Ubuntu 16 - Homestead and Forge installs at EC2 with PHP 7.0
#
# Notes:
#
# - Remove 'extension = mongodb.so' from your main php.ini, as it needs to 
#   load after other extensions. 
#
# - This adds both the MongoDB server and the php drivers. To install the
#   drivers only, comment-out "sudo apt-get install -y mongodb-org;".
#
###########################################################################
echo "MongoDB install script with PHP7 & nginx [Laravel Homestead/Forge]"
echo "Importing the public key used by the package management system";
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
echo "Creating a list file for MongoDB.";
echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
echo "Updating the packages list";
sudo apt-get update;
echo "Install the latest version of MongoDB";
sudo apt-get install -y mongodb-org;
echo "Fixing the pecl errors list";
sudo sed -i -e 's/-C -n -q/-C -q/g' `which pecl`;
echo "Installing OpenSSl Libraries";
sudo apt-get install -y autoconf g++ make openssl libssl-dev libcurl4-openssl-dev;
sudo apt-get install -y libcurl4-openssl-dev pkg-config;
sudo apt-get install -y libsasl2-dev;
echo "Installing PHP7 mongoDb extension";
sudo pecl install mongodb;
echo "adding the extension to your php.ini file";
echo 'extension = mongodb.so' | sudo tee /etc/php/7.0/mods-available/mongodb.ini
sudo ln -s /etc/php/7.0/mods-available/mongodb.ini /etc/php/7.0/fpm/conf.d/30-mongodb.ini
sudo ln -s /etc/php/7.0/mods-available/mongodb.ini /etc/php/7.0/fpm/conf.d/30-mongodb.ini
sudo service mongod start
echo "restarting The nginx server";
sudo service nginx restart && sudo service php7.0-fpm restart
###########################################################################
```
