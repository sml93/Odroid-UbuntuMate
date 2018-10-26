# Odroid-UbuntuMate
Odroid Setup for ROS (KINETIC) installation

## Bill of Materials
- Odroid XU4
- 128 GB eMMC Module for XU4
- WiFi Module
- Keyboard/Mouse (optional)

## First Time Ubuntu Setup (For eMMC w/o pre-installed image)
### Download and Flash Ubuntu (Mate)
Download the Ubuntu 16.04 LTS minimal or mate image from [hardkernel's official odroid wiki repo](https://wiki.odroid.com/odroid-xu4/os_images/linux/ubuntu_4.14/20171213)
Install [win32](https://sourceforge.net/projects/win32diskimager/) or [etcher](https://etcher.io/) to flash the image into your eMMC

## Network Setup
A network connection is required to complete the first-time setup after flashing the distro. As  `root`, do the following:\
`sudo apt-get gedit` to download an editor (optional)\
`sudo gedit /etc/network/interfaces` or `sudo nano /etc/network/interfaces` (if you did not install gedit) then add the following lines in:

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

Have you ensure that:
1) Display Manager - Greeter settings are okay?
2) Partitioning is allocated accordingly?


# ROS (KINETIC) Installation
#### Setup your sources list
`sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'`
#### Set up your keys
`sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116`
## Installation
`sudo apt-get update`
#### Desktop-Full Installation:
`sudo apt-get install ros-kinetic-desktop-full`
#### Desktop Installation:
`sudo apt-get install ros-kineti-desktop`
#### ROS-Base (Bare Bones)
`sudo apt-get install ros-kinetic-ros-base`
#### Individual Package
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


# To connect between multiple ROS machines (Odroid to Laptop(s))
## On Odroid
Power up the `odroid`

Open a terminal but pressing `ctrl+alt+t`

Run `roscore`

Open another tab `ctrl+shift+t` and `rosrun` an application

## On Laptop or Desktop or PowerShell
Boot into ubuntu, `ctl+alt+t`

`ssh odroid@192.168.1.126` (Odroid's ROS_IP)

> A message will be displayed, type `y` or `yes`

`env | grep ROS` and check if the IP address is entered (it should not be there)

`export ROS_IP=192.168.1.127` (exporting roscore machine's IP address)

`sudo gedit ~/.bashrc` (or sudo nano)

Open another tab/terminal and ssh into odroid again

Run `rostopic list` and check if you are able to see the list of topics on ROS MASTER


### Streaming serial Jevois on Odroid 
`ctrl+alt+t` + `guvcview`

`ctl+alt+t`

`sudo screen /dev/ttyUSB0 115200` 

You should see a string of data according to what mode you choose Jevois to run
