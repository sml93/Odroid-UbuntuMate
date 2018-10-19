# Odroid-UbuntuMate
Odroid Setup for ROS (KINETIC) installation

## Bill of Materials
- Odroid XU4
- 128 GB eMMC Module for XU4
- WiFi Module
- Keyboard/Mouse (optional)

## First Time Ubuntu Setup (For eMMC w/o pre-installed image)
### Download anf Flash Ubuntu (Mate)
Download the Ubuntu 16.04 LTS minimal or mate image from [hardkernel's official odroid wiki repo](https://wiki.odroid.com/odroid-xu4/os_images/linux/ubuntu_4.14/20171213)
Install [win32](https://sourceforge.net/projects/win32diskimager/) or [etcher](https://etcher.io/) to flash the image into your eMMC

## Network Setup
A network connection is required to complete the first-time setup after flashing the distro. As  `root`, do the following:\
`sudo apt-get gedit` to download an editor (optional)\
`sudo gedit /etc/network/interfaces` or `sudo nano /etc/network/interfaces` (if you did not install gedit) then add the following lines in:\
`auto wlan0`\
`allow-hotplut wlan0`\
`iface wlan0 inet dhcp`\
`wireless-power off`\
`wpa-ssid Free`\
`wpa-psk 748748748`

If you face an issue between Odroid XU4 and the wifi module, follow this instructions [here](https://adamscheller.com/systems-administration/rtl8192cu-fix-wifi/) to fix it

## User Account Setup
The minimal distribution only has `root` setup. To add our own account, `odroid`, use these commands:\
`adduser odroid`
`adduser odroid sudo`


# ROS (KINETIC) INSTALLATION
## Setup your sources list
`sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'`
## Set up your keys
`sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116`
## Installation
`sudo apt-get update`
### Desktop-Full Installation:
`sudo apt-get install ros-kinetic-desktop-full`
### Desktop Installation:
`sudo apt-get install ros-kineti-desktop`
### ROS-Base (Bare Bones)
`sudo apt-get install ros-kinetic-ros-base`
### Individual Package
`sudo apt-get install ros-kinetic-PACKAGE`\
To find available packages, use:\
`apt-cache search ros-kinetic`
## Initialise Rosdep
`sudo rosdep init`
`rosdep update`
## Environment Setup 
`echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc`\
`source ~/.bashrc`
## Dependencies for building packages
`sudo apt-get install python-rosinstall python-rosinstall-generator python-wstool build-essential`
