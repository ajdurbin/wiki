# Links
- <https://github.com/jupyterhub/jupyterhub>
- <https://github.com/jupyterhub/jupyterhub/wiki/Installation-of-Jupyterhub-on-remote-server>
- <https://jupyterhub.readthedocs.io/en/latest/quickstart.html#installation>
# Installation
```
adduser alex
usermod -aG sudo alex
apt-get install vim git python3 python3-pip npm nodejs-legacy -y
python3 -m pip install --upgrade pip
python3 -m pip install jupyterhub
npm install -g configurable-http-proxy
python3 -m pip install notebook
mkdir /root/jupyterhub
cd jupyterhub
# generate configuration file
/usr/local/binjupyterhub --generate-config
```

Make `/etc/systemd/system/jupyterhub.service` with the following contents:
```
[Unit]
Description=Jupyterhub
After=network.target

[Service]
RestartSec=2s
User=root
WorkingDirectory=/root/jupyterhub
ExecStart=/usr/local/binjupyterhub --no-ssl -f jupyterhub_config.py
Restart=always

[Install]
WantedBy=multi-user.target
```
Enable and start the service.
