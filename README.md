# Odroid-UbuntuMate
Odroid Setup for ROS (KINETIC) installation

## Bill of Materials
- Odroid XU4\
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
`wpa-psk 748748748`\

If you face an issue between Odroid XU4 and the wifi module, follow this instructions [here](https://adamscheller.com/systems-administration/rtl8192cu-fix-wifi/) to fix it

## User Account Setup
The minimal distribution only has `root` setup. To add our own account, `odroid`, use these commands:\
`adduser odroid`
`adduser odroid sudo`
\

# ROS (KINETIC) INSTALLATION
