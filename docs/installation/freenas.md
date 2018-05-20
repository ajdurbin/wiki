### Installation 
  - Requires two USB drives, for installation image and installation target
  - Choose FreeNAS installer, select USB drive for installation target
  - Fresh install, format boot device
  - Hardware password
  - BIOS booting
  - Reboot and remove installation media
  - Displays menu with IP for web GUI
  - Open web GUI, sign in with root, hardware password
  - Exit initial wizard
  - Change hostname to `huron.localdomain`, timezone to America/Detroit
  - `Storage -> Volumes -> Volume Manager` to create volume using all disks and ZFS RAID 0 or ZFS Striped
  - Create datasets, change user and group permissions to nobody, add write privileges to user/owner/group
  - Go to Sharing, select dataset, NSF share, change MapAll user and MapAll groups to nobody so it doesn't matter what user connects to the shares
  - To mount in Unix, `mount -t nfs freenasip:/mnt/volumenname/datasetname /path/to/mount`
  - Then unmount with `umount /path/to/mount`

### Plex Plugin 

  - Install the Plex plugin
  - Go to Jails -> plexmediaserver -> Add storage and add the necessary directories, be sure to choose 'create directory'
  - Go to Plugins -> Installed -> plexmediaserver and turn on
  - Then go to `http://plexpluginip:32400/web/` to access server
  - Note that first install attempt did not initiate a plex 'server' only a plex client and reinstallation was necessary


### Resilio Sync Plugin 
  - Install BTsync plugin
  - Create new dataset with write permissions for group, other with nobody:nobody the owner:group users
  - Add the new dataset under `/mnt` 
  - Open the GUI, username alex with software password
  - Add a read-only key from another host