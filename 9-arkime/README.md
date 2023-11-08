### install Arkime

### Elastic
1. Go to your Kibana
2. Stack Management > Roles
3. Create Role `arkime_role` and give it :
   - cluster privileges : monitor, manage_index_templates 
   - Index privileges `all` for indices `arkime*`
4. Go to your Kibana > Stack Management > Users > Create User
5. Add new user `arkime` and attach role `arkime_role`


### Arkime 

```shell
wget https://github.com/arkime/arkime/releases/download/v4.6.0/arkime_4.6.0-1.ubuntu2204_amd64.deb
sudo dpkg -i arkime_4.6.0-1.ubuntu2204_amd64.deb
sudo apt-get -f install -y
```

You will need to run `/opt/arkime/bin/Configure` script to setup Arkime. You can run it with the following command and with output:

Run command
```shell
sudo /opt/arkime/bin/Configure
```

Fill as follows:
```shell
Found interfaces: lo;ens5
Semicolon ';' seperated list of interfaces to monitor [eth1] ens5
Install Elasticsearch server locally for demo, must have at least 3G of memory, NOT recommended for production use (yes or no) [no] no
Elasticsearch server URL [http://localhost:9200] https://ingest-student13.threatlab.ninja 
Password to encrypt S2S and other things, don't use spaces [no-default] randomness
Arkime - Creating configuration files
Installing sample /opt/arkime/etc/config.ini
Arkime - Installing /etc/security/limits.d/99-arkime.conf to make core and memlock unlimited
Download GEO files? You'll need a MaxMind account https://arkime.com/faq#maxmind (yes or no) [yes] yes
Arkime - Downloading GEO files
2023-11-08 17:37:21 URL:https://www.iana.org/assignments/ipv4-address-space/ipv4-address-space.csv [23329/23329] -> "/tmp/tmp.gXTzXKTeDd" [1]
2023-11-08 17:37:21 URL:https://raw.githubusercontent.com/wireshark/wireshark/release-4.0/manuf [2195411/2195411] -> "/tmp/tmp.0npzvcUIKm" [1]

Arkime - Configured - Now continue with step 4 in /opt/arkime/README.txt

 4) The Configure script can install OpenSearch/Elasticsearch for you or you can install yourself
 5) Initialize/Upgrade OpenSearch/Elasticsearch Arkime configuration
  a) If this is the first install, or want to delete all data
      /opt/arkime/db/db.pl http://ESHOST:9200 init
  b) If this is an update to an Arkime package
      /opt/arkime/db/db.pl http://ESHOST:9200 upgrade
 6) Add an admin user if a new install or after an init
      /opt/arkime/bin/arkime_add_user.sh admin "Admin User" THEPASSWORD --admin
 7) Start everything
      systemctl start arkimecapture.service
      systemctl start arkimeviewer.service
 8) Look at log files for errors
      /opt/arkime/logs/viewer.log
      /opt/arkime/logs/capture.log
 9) Visit http://arkimeHOST:8005 with your favorite browser.
      user: admin
      password: THEPASSWORD from step #6

If you want IP -> Geo/ASN to work, you need to setup a maxmind account and the geoipupdate program.
See https://arkime.com/faq#maxmind

Any configuration changes can be made to /opt/arkime/etc/config.ini
See https://arkime.com/faq#arkime-is-not-working for issues

Additional information can be found at:
  * https://arkime.com/faq
  * https://arkime.com/settings
```

Init elasticsearch
```shell
sudo  /opt/arkime/db/db.pl --esuser arkime:arkimeuser https://ingest-student13.threatlab.ninja init
```

Note !
There seems to be some bug in the init script which occasionally doesn't properly add user.
To work around this you need to manually edit config file `/opt/arkime/etc/config.ini` and update following line:
```
elasticsearch=https://USERNAME:PASSWORD@ingest-studentX.threatlab.ninja
```
If you experience the same issue then just change the config and restart capture `systemctl restart arkimecapture.service`

create user 
```shell
sudo /opt/arkime/bin/arkime_add_user.sh admin "Admin User" STUDENTP2SSWORD --admin
```

add geoip database
```shell
sudo wget https://github.com/P3TERX/GeoLite.mmdb/raw/download/GeoLite2-ASN.mmdb -O /opt/arkime/etc/GeoLite2-ASN.mmdb
sudo wget https://github.com/P3TERX/GeoLite.mmdb/raw/download/GeoLite2-Country.mmdb -O /opt/arkime/etc/GeoLite2-Country.mmdb 
sudo wget https://raw.githubusercontent.com/wireshark/wireshark/release-4.0/manuf -O /opt/arkime/etc/oui.txt
```

start capture and viewer
```shell
sudo systemctl start arkimecapture.service
sudo systemctl start arkimeviewer.service
```

Go to your Arkime UI `http://studentX.ec2.threatlab.ninja:8005/` and login with `admin` and your provided password.