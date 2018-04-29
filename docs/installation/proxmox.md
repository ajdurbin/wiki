### Installation 
  - Grab latest Proxmox iso and boot from USB
  - Choose install
  - Select ZFS RAID 0 and choose hard drives, be sure to not include USB drive here
  - Change timezone to America/Detroit
  - Enter hardware password and email address
  - Change FQDN to `superior.localdomain`

### Configuration 
  - Comment out `deb https://enterprise.proxmox.com/debian/pve stretch pve-enterprise` in `/etc/apt/sources.list.d/pve-enterprise.list`
  - Add `deb http://download.proxmox.com/debian/pve stretch pve-no-subscription` to `/etc/apt/sources.list`
  - `apt-get update && apt-get dist-upgrade`
  - Add LXC templates at `Datacenter -> Superior -> local (superior) -> Content -> Templates`
  - If TurnKey templates are missing, do `pveam update`

### Mount FreeNAS NFS Shares On Boot 
  - Make subdirectories in `/mnt` named after datasets to be mounted, ie, `mkdir /mnt/torrents`
  - Edit `/etc/fstab` with `freenasip:/mnt/volume/datasetname   /mnt/datasetname   nfs    _netdev,auto  0  0`
  - Reboot and check file systems mounted properly

### Container Bind Mounts 
  - Edit `/etc/pve/lxc/<containerid>.conf` with `mp0: /proxmox/mount/path,mp=/container/mount/path`
  - Restart container and check `du -h` to see available storage
  - From `https://pve.proxmox.com/wiki/Linux_Container#_bind_mount_points` and `https://www.jamescoyle.net/how-to/2019-proxmox-4-x-bind-mount-mount-storage-in-an-lxc-container`

### Container SSH 

SSH isn't enabled in containers by default. For using a 'native' terminal instead of that included in the Proxmox GUI to SSH into a container, SSH into Proxmox then `lxc-attach --name <containerid>`. From `https://ping.flenny.net/2016/ssh-into-a-proxmox-lxc-container/`.

### Locale errors in lxc containers 

`locale-gen en_US.UTF-8`

### accidents 
installed git and mysql-server outside of container