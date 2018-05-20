### Installation 

`apt-get install mysql-server -y` with software password

Access SQL server with `mysql -u root -p` and type in password, then `drop table if exists gogs; create database if not exists gogs character set utf8 collate utf8_general_ci; exit`

`apt install git -y`

`wget` the tar file from gogs binary files and `tar zxf gogs.gz`

`cd gogs` and `./gogs web`

Go to `http://gogsip:3000`

Change run user to root

Add admin account settings with software password

Install and refresh page, will be logged in as admin account

For cloning/pushing/etc use HTTP instead of SSH and provide admin account and password until SSH keys are setup

Look into mirroring repository option instead of multiple pushes to BitBucket and GitHub





