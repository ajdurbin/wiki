### Installation 
  - Create new container using the TurnKey Torrent Server template with default HDD size and 4GB RAM, 1GB swap with software password
  - Starting container and logging in as root with software password begins the TurnKey GUI setup, use software password, skip automatic backups, skip email notifications, and install security updates
  - ruTorrent GUI is found at `https://torrentserverip:12322` with username admin and software password
  - Download directory is `/srv/storage/download`
  - Create mountpoint to FreeNAS dataset through Proxmox NFS mount by editing `/etc/pve/lxc/<containerid>.conf` with `mp0: /proxmox/nfs/mount,mp=/srv/storage/download`
  - Restart container
  - Check `du -h` afterwards to see newly available storage
  - From `http://www.beginninglinux.com/home/data-compression/unrar-all-files-from-multiple-subdirectories-at-once`, unrar a directory into another directory `unrar e -r -o- /path/to/torrents/*.rar /path/to/save/`.