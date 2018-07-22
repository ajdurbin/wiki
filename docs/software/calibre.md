# Links
* <https://www.digitalocean.com/community/tutorials/how-to-create-a-calibre-ebook-server-on-ubuntu-14-04>
* <https://calibre-ebook.com/download_linux>
* <https://manual.calibre-ebook.com/>
* <https://www.mobileread.com/forums/showthread.php?t=288408>

# Calibre Installation
```
apt-get install vim gcc-4.7 xvfb imagemagick git xdg-utils xz-utils python3 python3-pip -y
# might require apt-get update --fix-missing and reinstalling afterwards
mkdir /mnt/books
# shutdown and make mount point between host and container at /mnt/books
sudo -v && wget -nv -O- https://download.calibre-ebook.com/linux-installer.sh | sudo sh /dev/stdin
# ignore warning could not connect to display
# download some sample books to initialize database, should return add books message
wget http://www.gutenberg.org/ebooks/1342.kindle.noimages -O pride.mobi
wget http://www.gutenberg.org/ebooks/46.kindle.noimages -O christmascarol.mobi
xbfb-run calibredb add ./* --library-path /mnt/books
# remove books from cwd
rm ./*.mobi
# run
calibre-server /mnt/books
```

Make `/etc/systemd/system/calibre-server.service` with the following contents:
```
[Unit]
Description=Calibre
After=network.target

[Service]
RestartSec=2s
Type=simple
User=root
ExecStart=/opt/calibre/calibre-server "/mnt/books"
Restart=always

[Install]
WantedBy=multi-user.target
```
Start and enable the service

# Calibre-Web Installation
```
git clone calibre-web repository
cd calibre-web
python3 -m pip install --target vendor -r requirements.txt
# run for initial configuration
# change calibre database location, allow uploading, enable public registration
# might fail on submit - but re-running appears installation finalized
python3 cps.py
```

Make `/etc/systemd/system/calibre-web.service` with the following contents:
```
[Unit]
Description=Calibre-Web
After=network.target

[Service]
Type=simple
User=root
ExecStart=/usr/bin/python /root/calibre-web/cps.py

[Install]
WantedBy=multi-user.target
```
Start and enable the service.

