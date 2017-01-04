## Sync Server Time with Amazon NTP
Tested on Ubuntu 16 - Homestead and Forge

``` shell
###########################################################################
#
# Sync Server Time with Amazon NTP
# Tested on Ubuntu 16 - Homestead and Forge
#
###########################################################################
# This simply installs the NTP tool.
echo "Installing NTP...";
apt-get install ntp -y

# This replaces the default servers with Amazon NTP servers. Not necessary if you're not on AWS
echo "Updating NTP servers to Amazon...";
sed -i 's/.ubuntu.pool.ntp.org/.amazon.pool.ntp.org iburst/g' /etc/ntp.conf

# This will stop the service, force it to sync the clock immediately and then start it again.
echo "Syncing and restarting NTP...";
service ntp stop
ntpd -gq
service ntp start
echo "Update complete. NTP is now synced with Amazon!";

```
