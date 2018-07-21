# Installation #
- Install latest Raspbian Lite image
- `sudo raspi-config` to change username and enable ssh

# DokuWiki Configuration #
- `sudo apt-get update && apt-get install vim -y`
- `sudo apt-get install dokuwiki -y`. Will need to enter admin password and purge pages on removal.
- `sudo dpkg-reconfigure dokuwiki`. Here will be asked which webserer to use, document root address, local network or global network, purge packages on removal, make configuration/plugin directories web writeable, wiki title, license, and acl. Found at <http://techblog.danielpellarini.com/sysadmin/how-to-quickly-install-dokuwiki-on-debian/.>
- Afterwards edit `apache.conf` with `Allow from all`
- Restart Raspberry Pi
- Go to <http://raspberrypiip/dokuwiki/> and install MathJax plugin

# DokuWiki Backup #

Create `wikibackup.sh` with the following contents:

```
#!/bin/bash
# add namespaces as created
sudo sh -c "cp -r /var/lib/dokuwiki/data/pages/*.txt /home/pi/wiki/"
sudo sh -c "cp -r /var/lib/dokuwiki/data/pages/installation /home/pi/wiki/"
cd /home/pi/wiki
git add .
git commit -m 'wiki commit'
git push origin master
```

Then SSH into Raspberry Pi and backup with `/home/pi/wiki/wikibackup.sh`. Making this a daily cron job is difficult because of the `sudo sh -c` commands. Will continue to look for solutions for auto-commiting wiki updates.

