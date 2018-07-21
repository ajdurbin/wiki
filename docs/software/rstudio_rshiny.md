# Installation #

Following the excellent tutorial from <https://deanattali.com/2015/05/09/setup-rstudio-shiny-server-digital-ocean/#safety-first>

```
adduser alex
gpasswd -a alex sudo
su - alex

# install R
sudo sh -c 'echo "deb <http://cran.rstudio.com/bin/linux/ubuntu> xenial/" >> /etc/apt/sources.list'
gpg --keyserver keyserver.ubuntu.com --recv-key E084DAB9
gpg -a --export E084DAB9 | sudo apt-key add -
sudo apt-get update
sudo apt-get install r-base -y

# common dependencies for R packages
sudo apt-get install libcurl4-gnutls-dev libxml2-dev libssl-dev -y

# install packages using this method so they're able to be installed for shiny user
sudo su - -c "R -e \"install.packages('devtools', <repos='http://cran.rstudio.com/')\"">
sudo su - -c "R -e \"install.packages('rmarkdown', <repos='http://cran.rstudio.com/')\"">
...

# install rstudio server
sudo apt-get install gdebi-core -y
wget <https://download2.rstudio.org/rstudio-server-1.1.442-amd64.deb>
sudo gdebi rstudio-server-1.1.442-amd64.deb
# go to <http//ip:8787> for gui

# install shiny server
sudo su - -c "R -e \"install.packages('shiny', <repos='http://cran.rstudio.com/')\"">
wget <https://download3.rstudio.org/ubuntu-14.04/x86_64/shiny-server-1.5.7.907-amd64.deb>
sudo gdebi shiny-server-1.5.6.875-amd64.deb
# check homepage at <http://ip:3838>

# set up proper user permissions to share /srv/shiny-server/ between user and shiny user
sudo groupadd shiny-apps
sudo usermod -aG shiny-apps alex
sudo usermod -aG shiny-apps shiny
cd /srv/shiny-server
sudo chown -R alex:shiny-apps .
sudo chmod g+w .
sudo chmod g+s .

# make /srv/shiny-server/ a git repository for pulling apps
# have shiny-server repo in home folder and push to repo before pulling in /srv/shiny-server/ for running
sudo apt-get install git -y
cd /srv/shiny-server/
git init
```

We can also host interactive R Markdown documents if they're named `index.Rmd` with `runtime: shiny` in the YAML header.
