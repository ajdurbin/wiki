# Installation #

- <https://github.com/jupyter/nbviewer>
- <https://hub.docker.com/r/jupyter/nbviewer/~/dockerfile/>

The repository isn't the best resource, but through trial and error I got this to work.

```

apt-get update
apt-get install -y -q \
build-essential \
gcc \
git \
libcurl4-openssl-dev \
libmemcached-dev \
libsqlite3-dev \
libzmq3-dev \
make \
nodejs \
nodejs-legacy \
npm \
pandoc \
python3-dev \
python3-pip \
sqlite3 \
zlib1g-dev \
apt-get clean
git clone <https://github.com/jupyter/nbviewer.git>
cd nbviewer
apt-get install python3-pip -y
pip3 install -r requirements.txt
pip3 install -r requirements-dev.txt
pip3 install markdown
pip3 install statsd
npm install
invoke bower # raises exception for UnicodeDecodeError but works all the same?
invoke less
python3 -m nbviewer --debug --no-cache
```

Tried to manually install the npm packages (bower, less, less-plugin-autoprefix, less-plugin-clean-css, watch) using -g switch, but still UnicodeDecodeError persists.

Added the following `/etc/rc.local/`, `cd nbviewer; python3 -m nbviewer --debug --no-cache` to start on boot, but not able to access the console afterwards with this method, need to read more on running things as a background process here.
