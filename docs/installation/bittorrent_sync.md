### Installation And Configuration 
  - Create a new container on Superior
  - Do `echo "deb http://linux-packages.resilio.com/resilio-sync/deb resilio-sync non-free" | tee /etc/apt/sources.list.d/resilio-sync.list`
  - Do `wget -qO - https://linux-packages.resilio.com/resilio-sync/key.asc | apt-key add -`
  - Do `apt-get update && apt-get install resilio-sync`
  - Edit `/usr/lib/systemd/user/resilio-sync.service` with `WantedBy=default.target`
  - Enable the service `systemctl --user enable resilio-sync`
  - Change web GUI listening interface `./rslsync --webui.listen 0.0.0.0:8888`
  - Go to `http://bittorrentsyncip:8888` with username alex and software password
  - Add syncing folder under `/home/rslsync/btsync`