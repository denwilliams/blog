---
layout: post
title: Raspberry Pi Headless Install In a Nutshell
tags: [raspberrypi, raspbian]
---

A concise guide for people who don't need trivial things explained...

1. Download the latest _lite_ image from here: https://www.raspberrypi.org/downloads/raspbian/
2. Identify the disk number using `diskutil list`
3. Unmount the disk using diskutil, eg: `diskutil unmountDisk /dev/disk4`
4. Clone the image to the SD card, eg: `sudo dd bs=1m if=2016-03-18-raspbian-jessie.img of=/dev/rdisk4`
5. Eject the disk, eg: `sudo diskutil eject /dev/rdisk3`
6. Connect the Pi using an ethernet cable and boot from the new SD card
7. Find the IP address of the Pi from the DHCP server
8. Log in to the terminal using SSH (user _pi_, password _raspberry_), eg: `ssh pi@192.168.0.123`
9. Check which wireless networks are visible: `sudo iwlist wlan0 scan | grep ESSID`
10. Edit the wireless config: `sudo nano /etc/wpa_supplicant/wpa_supplicant.conf`

```
network={
    ssid="MyNetwork"
    psk="s00perS3cure"
}
```

11. Check if connected: `ifconfig wlan0`
12. Set a DHCP reservation for the MAC of the wireless adapter
13. Restart the adapter (`sudo ifdown wlan0 && sudo ifup wlan0`) or `pi sudo reboot`
14. Run `sudo raspi-config`, expand the filesystem and set internationalization options

UPDATE:

wpa_supplicant.conf now requires country code, eg:

```
country=US
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
    ssid="MyNetwork"
    scan_ssid=1
    psk="s00perS3cure"
    key_mgmt=WPA-PSK
}
```
