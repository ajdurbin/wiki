# Installation #

```
apt install git -y
wget -O gitea <https://dl.gitea.io/gitea/1.4/gitea-1.4-linux-amd64>
chmod +x gitea
./gitea web
```

Choose SQLite3 database and install after setting up admin account, also change Application URL, Domain to IP address instead of localhost.

Root user okay for running, but setup ssh keys or else you cannot clone/push to a repository over SSH.

Add `/root/gitea web` to `/etc/rc.local` before `exit 0` to start on boot

# Better Installation Links As Service #
- <https://docs.gitea.io/en-us/install-from-binary/>
- <https://docs.gitea.io/en-us/linux-service/>
- <https://github.com/go-gitea/gitea/blob/master/contrib/systemd/gitea.service>
