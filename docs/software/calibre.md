### Calibre Installation 

`sudo -v && wget -nv -O- https://download.calibre-ebook.com/linux-installer.sh | sudo sh /dev/stdin` gives a broken pipe error. Alternatively, use `apt-get install calibre`. Then start the application with `calibre-server` and go to port `8080`.

### Calibre-Web Installation 

Clone `https://github.com/janeczku/calibre-web` and then `python-pip` with `pip install --target vendor -r requirements.txt` then `nohup python cps.py` and go to port `8083` with username admin and password admin123. Set the location of the Calibre database `metadata.db` to `/mnt/books/` and submit. Edit `/etc/rc.local` with the appropriate python call to start server on boot. Make sure to add upload books option in configuration. Upload books using GUI and be sure to use find metadata option to get correct description, titles, book cover, etc.