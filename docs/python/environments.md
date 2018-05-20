### Usage 
To resolve package conflict issues, it's best to make a separate Python environment for each project. This way, we can explicitly specify our package versions and not worry about global package or package version conflicts.

Create a directory for your project and then create the virtual environment with `virtualenv -p python3 targetdirectory`

Activate the environment with `source targetdirectory/bin/activate`

From here, install packages using `pip3 install packagename`

To then make a file with all installed packages and their exact version numbers do `pip3 freeze -r > requirements.txt`

Then when creating a new environment and want to install the same exact packages, use `pip install -r requirements.txt`

### LXC Containers 
LXC Ubuntu containers should have Python 3.5 installed, but PIP will also need to be installed by install locales with `locale-gen en_US.UTF-8` and then `apt install python3-pip`.