# Installation 
```
apt-get install git vim -y

# create service user
adduser \
   --system \
   --shell /bin/bash \
   --gecos 'Git Version Control' \
   --group \
   --disabled-password \
   --home /home/git \
   git
su git
# get binary
wget -O gitea https://dl.gitea.io/gitea/1.4.3/gitea-1.4.3-linux-amd64
chmod +x gitea
cd gitea
# initialize application
# sqlite3 database, change localhost to container IP, create admin user
# require sign-in to view pages, enable captcha
./gitea web
```
Make `/etc/systemd/service/gitea.service` with the following contents under `root`:
```
[Unit]
Description=Gitea
After=syslog.target
After=network.target

[Service]
RestartSec=2s
Type=simple
User=git
Group=git
WorkingDirectory=/home/git
ExecStart=/home/git/gitea web -c /home/git/custom/conf/app.ini
Restart=always

[Install]
WantedBy=multi-user.target
```
Enable and start the service.

# Better Installation Links As Service
- <https://docs.gitea.io/en-us/install-from-binary/>
- <https://docs.gitea.io/en-us/linux-service/>
- <https://github.com/go-gitea/gitea/blob/master/contrib/systemd/gitea.service>
