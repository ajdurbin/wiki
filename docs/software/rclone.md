# Installation #

- Create a new Ubuntu container and follow the directions from <https://rclone.org/install/> after installing `curl, unzip`
- Copy `.rclone.conf` to the home directory
- Add the appropriate NFS directories as necessary for uploading
- Install `tmux` to attach sessions as needed (Not working in LXC containers for some reason)
- Upload data using `nohup rclone copy /source/path remote:/dest/path &`
