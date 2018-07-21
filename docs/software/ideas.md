# About #

This page is to log different software packages with short descriptions for possible later inclusion in my home lab. A lot of these will be from <https://github.com/Kickball/awesome-selfhosted.>

# Virtualization #
- Docker
- lxc
- Proxmox

# File Syncing #
- Resilio-Sync: Has Android/iOS applications and FreeNas plugin. Works well enough even though user permissions on installation are weird. Closed source.
- Syncthing: Has Android/iOS applications. Documentation not great for steps after installation to actually sync the folders from one site to another.
- RClone: Powerful tool for syncing folders/files to Google Drive. Great documentation.
- rsync: Command line tool for syncing folders or files one way or both ways with deletion or not.
- NextCloud: Selfhosted Google Drive replacement with Calendar, instant messaging support, etc.

# Machine Learning and Statistics #
- comet.ml: Cool utility for sharing models with other's including documentation, git support, etc.
- gluon: AWS/Microsoft tool similar to comet.ml
- TensorBoard: Visualize statistics from TensorFlow models.
- nbviewer: view notebooks from git repository as a website or using a static site generator
- jupyter hub: Jupyter notebook server and Python kernel for multiple users
- RStudio Server: R server with web GUI
- R Shiny server: Server for selfhosting R Shiny applications

# Visualizations #
- Grafana

# Databases #
- Graphite
- influxdb
- Kafka
- Cassandra
- Hadoop/Spark

# Web services #
- reverse proxy to safely expose applications to outside world or just static site
- Redis for server side caching for web applications

# Data Collection #
- Owntracks
- OpenWeatherMap
- openstreetmap
- personal statistics
- CTV
- timed still-shot photos of outdoors

# CI/CD #
- Artifactory to store images
- Jenkins to build images from git repository
- kubernetes to deploy docker applications
- Internal pypi repository

# Entertainment #
* Plex
* plex channels
* Sonarr
* Jacket
* Radarr
* Calibre
* Minecraft server
* Insurgency server?

# tools #
- zabbix for monitoring hosts
- internal dns server besides pfsense host?
- authentication like FreeIPA
- IP phones, FreePBX

# HPC #
* slurm/torque/whatever job schedular
* environment modules for different software versions
* mpi
* mp

# Communication #
* Discord
* IRC
* RSS

# word salad #
* todo list outside wiki
* use Google Calendar more, contacts for address book
* chatbot
* Mkdocs wiki behind reverse proxy and pushed to github pages or readthedocs (can remove signature that bugs me) with notebooks on github provided to nbviewer in some notebook repository
* owntracks behind <https>
* zabbix statistics
* graphite stats exported from freenas, proxmox very easily, push to grafana
* shiny reverse proxy
* github tags for model passing pypi, etc
* selfhosted git and push to bitbucket, github also
* merge both data analytics repositories
* make a notebook repository and copy files there
* make notebook viewer application
* link notebooks from github to nbviewer online
* upload all of grad school stuff to repos, do some cleaning up of miscellaneous notebook ones with better names
* raspberry pi mkdocs installation
* statistics and deep learning should all be single directory in new wiki
* get back into journal
* customizing bashrc, put bashrc rcprofile, any relevant config files in unix directory, reverse proxy files
* DUO two factor
* mkdocs gh-deploy for new documentation, poor performance on raspberry pi and annoying editing documents in real time with log files printed to screen, okay with running in vm or not? Deploying to github messed up personal website root, so also need to see if I'm fine not having personal website or not or including in new documentation.
* Use gitea instead of gogs and figure out ssh key situation for pushing since it's getting annoying using passwords
* reorganize python folders for notebook viewer
* create snippets repository like Bob Settlage?
* Rstudio/rshiny server in single machine
* jekyll for github pages, maybe that's okay to have github root page jekyll with wiki backend if single page?
* Try reverse proxy of shiny applications, wiki
* Fetch ASC code from Peter's repository since we worked on these things and there are lots of examples
* Journal? switch to python package or keep using Rmd
* Graphite/grafana fetch statistics from huron, superior maybe separate instance for open weather map
* own tracks
* travic ci instead of jenkins, need to figure out local installation
* kubernetes on superior root
* ci/cd pipeline with git -> jenkins/travisci -> artifactory -> kubernetes deployment
* unit testing with tox, other python packages
* list of standard R packages
* heroku
* redis server for web caching
* alpine linux images
* fix annoying windows/ubuntu dual boot time issue
* blender for 3d modeling
* look more into python parallel/distributed computing packages
* if pushing code to github always make a gh-pages branch with some docs in it to be pushed too, at least for some longer projects for nicer to read stuff
* git web hooks
* combine statistics/ml/dl/nlp pages into single directory
* github pages personal page can't be with subdirectories, so try having only single top level page. mkdocs routing to convert dokuwiki text, need to rename start to index
* Manual mkdocs gh-deploy routine with ssh keys and checkout
* sample project to test sphinx functionality?
* continue using dokuwiki on pi (just so it can be used), and then convert files to mkdocs for github pages for outside usage?
* webhooks to trigger ci/cd pipelines
* web service for hosting applications from flask/tornado/gnuicorn
* heroku/pythonanywhere
* mongo/mariadb instead of mysql - recall <https://www.reddit.com/r/AskReddit/comments/8fztrk/what_was_the_removing_the_headphone_jack_of/> and discussion of Oracle no longer developing mysql basically
* full virtualmachine with docker installed as docker host
* jenkins dockerfile github to artifactory and docker using travis ci when can
* appears that marathon is only for mesos-based systems
* kubernetes?
* traefik
* "hacking" fake terminal
* calibre server for ebooks
* get docker jenkins git pipeline first before worrying about artifactory
* load balancer
* internal dns
* docker swarm/compose versus a kubernetes solution
* some sort of docker load balancing
* docker traefik
* gitlab has their own ci/cd stuff similar to jenkins/travis-ci
* bettercodehub
* static site generators like Hugo
* reverse proxy for non-static sites, like dokuwiki for instance or any other php web application
* digital ocean tutorials
* teraform
* caddy server
* haproxy
* freeipa
* freepbx
* reddit raspberry pi ups server tutorial
* recipe manager
* docker spark/hadoop images
* sonarqube
* reverse proxy notebooks
* static site generator usage
* how are interactive applications served?
* cassandra data model
* sql data model
* selfhosted gitbook? and if so vs bookdown
* nvidia jetson for embedded deep learning machine - but uses proprietary ubuntu distribution
* raspberry pi compute module/camera/
* intel movidius vpu neural compute engine
* time lapse
* data labelling application
* open street map
* gis open data
* information retrieval
* selfhosted pypi (pypiserver package easy setup)
* selfhosted docker registry (would like to get the ssl setup working)
* lets encrypt web server for generating certifcates and static sites
* bookdown vs gitbook vs pandoc
* graylog
* haproxy
* honeypots
* gitlab account - should be free and private for university students
* google collaboratory, online jupyter notebooks with gpu usage!!!
* letsencrypt wildcard subdomains
* intel movidius neural compute module for small board computers like raspberry pi, though may not support keras
* armbian/rock64/debian cheap hardware page discussing sbc. Rasberry Pi is just best supported though.
* nanoleaf smart wall light panel, pretty cool
* weex opens ource weather software has a supported hardware page with lots of cool weather kits
* gimp photo processing
* blender 3dmodeling
* spaceengine.org
* stud.io lego modeling program
* bricklink
* draw.io
* blob storage for database byte storage, say images
* mongo, arongo databases
* graph architecture vs key vs relational database
* hdfs
* elastic
* luminoth open source computer vision toolkit for bounding boxes and confidence
* ilastix image segmentation tool interactive
* blue iris windows only alternative to zoneminder that everyone loves
* bookmarks selfhosted or read later list, also have shared tabs between chrome on pc, laptop, ubuntu?
* personal jira task list
* traefik reverse proxy for docker
* mqtt
* freedns reverse proxy subdomains
* code ocean for sharing reproducible scientific computing
* strava for tracking bike rides
* opentoonz
* open broadcasting software - obs or whatever everyone uses for streaming
* squeeky wheel complain on twitter of internet speed slow
* ngrok
* semver.org for software release versioning
* mybinder.org
* bigquery public datasets
* dont dump every software install into rc.local to run on boot, make it into a unix service, go back through various installations that were put into rc.local and add & to gracefully exit the file.
* swagger free service to visualize api calls
* <http> request methods for web services/api: <https://www.w3schools.com/tags/ref_httpmethods.asp>
* traefik for reverse proxy and load balance microservices lock docker containers, Nick K from A-O is interested in using this with authentication and with a domain.
* rocketchat as a slack alternative
* elasticsearch
* python anywhere
* read it later list - like wallabag is most popular
* rss reader like tiny tiny rss for lots of stuff, find more uses for rss
* source control any configuration files changes on any services for easy backup and restoration
* marktext cool markdown editor with lots of features
* <https://hipstercat.fr/gogs/hipstercat/rudead> send messages to relatives after dying, idea is for all those passwords and information they'd need to find that you could provide easily
* openlogos
* <https://paperswithcode.com/>
* house hunters plot twitter robot, very funny
* <https://medium.mybridge.co/machine-learning-open-source-of-the-month-v-may-2018-efd396d9306e>
* <https://mitpress.mit.edu/sites/default/files/sicp/index.html> software design book
* object oriented thought process
* <https://erlemar.github.io/> lists the different projects they've worked on
* choosealicense.com
* gitignore.io
* <https://thehftguy.com/2016/10/24/heres-how-to-make-a-good-github-project-for-your-resume/>
* ai train for simple video game
* <https://medium.com/@marcelogdeandrade/writing-your-own-programming-language-and-compiler-with-python-a468970ae6df>
* oeisbot reddit bot for presenting sequences
* gravatar
* <http://lightning-viz.org/>
* snibox as a snippet repository and web gui, can tag snippets
* open source api gateways
* static sites
* markdown
* graph vs relational vs nosql databases
* sql database design 1-to-many, many-to-1 relationships
* venmo twitter bot tweats drug deals
* openheatmap/leaflet/candela/charted/datawrapper/rawgraphs/d3.js/plotly/dygraphs
* <https://engineering.videoblocks.com/web-architecture-101-a3224e126947> great explanations on web server stacks
* openid
* kerberos authentication
* kubernetes
* <https://developer.okta.com/blog/2018/07/12/flask-tutorial-simple-user-registration-and-login> openid for flask authentication
* drone has marathon plugin
* openid/oauth for universal authentication
* google analytics tracking information

Main goal is to get working git-jenkins-artifactory-docker plugin going. So we'd have a remote git repository to trigger a jenkins build that tests the software before sending to artifactory and then deploying on the docker server. So the jenkins file will be split up to be build the image using docker server, then push image to docker registry, then pull image from docker registry and run.

Do more scientific computing so go back to learning a compiled code framework, more R shiny stuff, MCMC, Bayesian stats, maybe go back to C++ to do some CUDA, more web development with Flask/Django

This is a great tutorial: <https://medium.com/bettercode/how-to-build-a-modern-ci-cd-pipeline-5faa01891a5b> and somewhat related <https://medium.com/@evheniybystrov/continuous-delivery-of-react-app-with-jenkins-and-docker-8a1ae1511b86>

__Plan__: Put Jenkins on Docker host and use Docker's built in registry, look into Docker git server that's lightweight enough. Use these for development and then push applications to Heroku and use travis-ci for Github.
