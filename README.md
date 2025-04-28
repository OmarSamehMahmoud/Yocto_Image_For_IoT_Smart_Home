# Building Yocto Custom Image For IoT Smart Home.
* ➢Build yocto image for raspberry pi to control our home with full system of lighting, opening doors ,opening air coordinator ,fans as cooling system ,fire alarm and temperature monitoring interact with website and firebase (real time database).


## Overview
The Yocto Project stands as a collaborative effort under the Linux Foundation, aiming to develop tools and methodologies for building Linux distributions suitable for embedded systems and IoT applications. Its objective is to provide a framework independent of the underlying hardware architecture.

## Prerequisites
* Ensure you have a minimum of 50 GB free disk space available.

## 1. Installation of Dependencies
```bash
sudo apt-get install gawk wget git-core diffstat unzip texinfo gcc-multilib \
build-essential chrpath socat cpio python3 python3-pip python3-pexpect \
xz-utils debianutils iputils-ping python3-git python3-jinja2 libegl1-mesa libsdl1.2-dev \
pylint3 xterm
```

## 2. Yocto Repository Cloning
```bash
git clone -b kirkstone  git://git.openembedded.org/meta-openembedded --depth=1
```

## 3. Retrieving Raspberry Pi Meta Layer
```bash
cd poky/
git clone  -b dunfell https://github.com/agherzan/meta-raspberrypi.git --depth=1
```

## 4. Configuration Steps for Poky (rpi4-64)

### 4.1 Environment Setup Script Execution
Run the provided script to establish the environment. This will create a directory named 'build'.
```bash
source oe-init-build-env
cd conf/
```

### 4.2 Editing Local Configuration
Open the 'local.conf' file using your preferred text editor.
```bash
gedit local.conf &
```

### 4.3 Adjusting Machine Variable
Edit the 'MACHINE' variable to reflect your machine's name.
```conf
MACHINE ??= "raspberrypi4-64"
```

### 4.4 Defining Image Formats
Add the 'IMAGE_FSTYPES' variable to generate 'sd_img' for later use.
```conf
IMAGE_FSTYPES = "tar.xz ext3 rpi-sdimg"
```

### 4.5 Enabling UART Connection
Set the 'ENABLE_UART' variable to '1' to enable USB-TTL connection if required.
```conf
ENABLE_UART = "1"
```

### 4.6 Adding Additional Packages
Append desired packages to the 'IMAGE_INSTALL' variable.
```conf
IMAGE_INSTALL_append = "openssh"
```

## 5. Integration of Meta-RaspberryPi Path
Include the path to 'meta-raspberrypi' in the 'bblayer.conf' file.

## 6. Building the Yocto Image
* This process may consume considerable time, approximately 2-3 hours on a robust system.
* Ensure a stable and high-speed internet connection to prevent interruptions.
```bash
bitbake core-image-minimal -k
```
