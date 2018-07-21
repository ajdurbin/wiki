# Installation #

- Download latest Ubuntu LTS image and burn to USB
- Boot PC into BIOS and under Boot Options choose UEFI: USB_NAME to boot Ubuntu live image, then choose try Ubuntu without installing
- Open GParted and ignore the Libparted warning about physical block size
- Carefully choose /dev/sd* corresponding to the SSD boot drive
- Choose the linux-swap partition and right-click and select Swapoff, this will redo the Libparted warning about physical block size after rescanning the partitions
- Right-click and delete both partitions separately, then hit the green check mark in GUI to apply these pending operations
- It deletes partitions and again raises the Libparted warning
- Exit GParted
- Double click on install ubuntu icon
- English -> Continue
- Download updates or proprietary drivers during installation (not doing so gives broken screen on login)
- Choose install ubuntu alongside windows boot manager
- Install now, continue to write changes to disk
- Set Detroit, MI
- Give name, pc name, username, hardware password, require password to login
- Restart when completed, it will prompt for removal of installation media before rebooting
- Windows 10 is accidentally prioritized on boot, so need to boot back into BIOS and choose the GRUB partition as highest priority.
- Will possibly get a black or broken screen on restarting
- Per <https://askubuntu.com/questions/760934/graphics-issues-after-while-installing-ubuntu-16-04-16-10-with-nvidia-graphics> follow option 3
- Reboot into GRUB, highlight Ubuntu option and press `e`
- Add `nouveau.modeset=0` to the end of the line beginning with `linux`
- Press `F10` to boot
- If still black or broken screen after rebooting
- `Ctrl Alt F1` opens a new console
- `sudo apt-get purge nvidia-*`
- `sudo add-apt-repository ppa:graphics-drivers/ppa`
- `sudo apt-get update`
- `sudo apt-get install nvidia-384` (or the latest Nvidia driver)
- Reboot and graphics issues should be solved
- Fix miscellaneous settings
- Install Google Chrome `.deb` with `sudo dpkg -i google-chrome...` with an intermediate install fix with `sudo apt-get install -f` after first failing
- Install Vim, Git, KeePass, HTop, Tmux with `sudo apt-get install -y vim htop tmux keepass2 git`
- Sound may not work immediately, open All Settings -> Sound and 'Test Sound' usually fixes this
- Choosing Detroit as location at installation results in package updates and installation from Ubuntu's Cananda mirrors, going to Software & Updates and choosing 'Download from: Main server' fixes this

# CUDA 9.0 Installation #
- Download Cuda 9.0 network `.deb` file
- Follow installation guide at <http://developer.download.nvidia.com/compute/cuda/9.0/Prod/docs/sidebar/CUDA_Installation_Guide_Linux.pdf>
- Verify CUDA-capable GPU with `lspci | grep -i nvidia`
- Verify support Linux version with `uname -m && cat /etc/*release`
- Verify gcc is installed `gcc --version`
- Verify correct kernel headers and development packages with `uname -r` then do `sudo apt-get install linux-headers-$(uname -r)`
- Install repository meda-data with ` sudo dpkg -i cuda-repo <distro>_<version>_<architecture>.deb`
- Install CUDA public GPG key with `sudo apt-key adv --fetch-keys
<http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub>
- `sudo apt-get update && sudo apt-get install cuda-9-0` (or whatever version TensorFlow requires)
- `cuda-command-line-tools` will be installed
- Older `nvidia- libcuda1 nvidia-opencl-icd` will be removed and replaced with newer versions
- Add path to PATH variable ` export PATH=/usr/local/cuda-9.0/bin${PATH:+:${PATH}}`
- Since we used `.deb` installation, the following doesn't modify the path, but to be safe do `export LD_LIBRARY_PATH=/usr/local/cuda-9.0/lib64\
${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}`
- Install writable samples with `cuda-install-samples-9.0.sh <dir>`, change into the directory, and `make`
- Compiling will take a file and some warnings or errors will be present, most are the result of the wrong CUDA version or environment variable in the code
- The old `nvidia-` graphics driver will still be present, so running `deviceQuery` will fail, restarting will show the newly installed `nvidia-` driver and `deviceQuery` will pass
- Add the PATH export statemnts to `.bashrc`
- Skip the Nsight plugin step
- Third-party libraries should already be installed
- Skip cuda-gdb installation
- In the 9.0 guide, ther Persistence Daemon installation is not included, but is in version 9.1, if necessary add `/usr/bin/nvidia-persistenced --verbose`

# cuDNN 7.0 Installation #
- Download all `.deb` files, ie, runtime, developer, and example files
- Do `sudo dpkg-i libcudnn7...` for each starting with the runtime library, then developer library, then documentation and examples
- Verify installation with example
- `cp -r /usr/src/cudnn_samples_v7/ $HOME`
- `cd $HOME/cudnn_samples_v7/mnistCUDNN`
- `make clean && make`
- `./mnistCUDNN`
- If properly running, should see a "Test passed!" or similar message
- Add `export CUDA_HOME=/usr/local/cuda` to `.bashrc`

# TensorFlow With GPU Support Installation #
- Follow <https://www.tensorflow.org/install/install_linux>
- `cuda-command-line-tools` were already installed, so need only add its path to environment, `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-9.0/extras/CUPTI/lib64` in `.bashrc`
- Use "Virtualenv" installation mechanism
- Install pip, virtualenv, and python-dev with `sudo apt-get install python3-pip python3-dev python-virtualenv`
- Create a virtual environment `virtualenv --system-site-packages -p python3 targetdirectory`
- Activate the environement `source ~/tensorflow/bin/activate`
- Install with `pip3 install --upgrade tensorflow-gpu`
- Validate the installation with ```import tensorflow as tf
hello = tf.constant('Hello, TensorFlow!')
sess = tf.Session()
print(sess.run(hello))
```
- Deactivate environment `deactivate`
- To uninstall TensorFlow, `rm -r targetdirectory`

# HDF5 #
For Keras features such as model saving to disk and using pre-trained models, this file system is necessary. Install it with `sudo apt-get install libhdf5-serial-dev`, which should install all the different HDF5 packages necessary. Then do `pip install hd5py` in your virtual environment. A warning will appear when using TensorFlow and models can be saved, however doing `hd5py.run_tests()` will fail. So this appears to be a non-issue for our uses.

# cv2 #
Also needed for deep learning is the `OpenCV` package. In source directory install with `pip install opencv-python`.


# R installation #
* follow <https://mran.microsoft.com/documents/rro/installation>
* download the gzip from Microsoft website
* `tar -xf microsoft-r-open-3.4.4.tar.gz`
* `sudo microsft-r-open/install.sh` and follow installation prompts, be sure to say yes to the MKL libraries
* Download the Rstudio .deb file and install with `sudo dpkg -i ...`, there will be an intermediate install step before working the second time

# Docker installation #

Follow <https://docs.docker.com/install/linux/docker-ce/ubuntu/>
```
sudo apt-get update
sudo apt-get install \
<apt-transport-https> \
ca-certificates \
curl \
software-properties-common
curl -fsSL <https://download.docker.com/linux/ubuntu/gpg> | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo add-apt-repository \
"deb [arch=amd64] <https://download.docker.com/linux/ubuntu> \
$(lsb_release -cs) \
stable"
sudo apt-get update
sudo apt-get install docker-ce
sudo groupadd docker
sudo usermod -aG docker $USER
sudo systemctl enable docker
sudo service docker start
# logout/login
docker run hello-world
```

# Heroku Installation #
`curl <https://cli-assets.heroku.com/install-ubuntu.sh> | sh` and type password when prompted

# Fix dual boot time difference #
An annoying thing when dual booting with Windows 10 is that after using Ubuntu and then booting Windows, the time will be off. Easiest solution is to set Ubuntu to use local time and rely on Windows for UTC.
```
timedatectl set-local-rtc 0 --adjust-system-clock # turn utc off
timedatectl set-local-rtc 1 --adjust-system-clock # turn utc on
```
From <https://www.howtogeek.com/323390/how-to-fix-windows-and-linux-showing-different-times-when-dual-booting/>
