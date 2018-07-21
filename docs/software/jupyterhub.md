# Installation #

Following the documentation from
- <https://github.com/jupyterhub/jupyterhub>
- <https://github.com/jupyterhub/jupyterhub/wiki/Installation-of-Jupyterhub-on-remote-server>
- <https://jupyterhub.readthedocs.io/en/latest/quickstart.html#installation>

```
adduser alex
usermod -aG sudo alex
apt-get install python3-pip npm nodejs-legacy -y
npm install -g <configurable-http-proxy>
pip3 install jupyterhub
pip3 install --upgrade notebook
jupyterhub --no-ssl
```

Instance is at <http://ipaddress:8000.>

Add `jupyterhub --no-ssl` to `/etc/rc.local` to start on boot

There are further options in a configuration file that require more reading on authentication measures, etc. But this was more of a want to do then need to do, probably won't use this often with michigan having a GPU.

# service #
- <https://github.com/jupyterhub/jupyterhub/wiki/Installation-of-Jupyterhub-on-remote-server>
