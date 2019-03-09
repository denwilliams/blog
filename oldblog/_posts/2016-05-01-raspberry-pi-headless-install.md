---
layout: post
title: Raspberry Pi Headless Install In a Nutshell (Mac)
tags: [raspberrypi, raspbian]
---

A concise guide for people who don't need trivial things explained...

1. Download the latest _lite_ image from here: https://www.raspberrypi.org/downloads/raspbian/
2. Identify the disk number using `diskutil list`
3. Unmount the disk using diskutil, eg: `diskutil unmountDisk /dev/disk4`
4. Clone the image to the SD card, eg: `sudo dd bs=1m if=2016-03-18-raspbian-jessie.img of=/dev/rdisk4`
5. Add an empty file `ssh` to the newly created drive's boot partition should be visible at `/Volumes/boot`
6. Eject the disk, eg: `sudo diskutil eject /dev/rdisk3`
7. Add the wireless configuration file `wpa_supplicant.conf` to the boot volume. (Note: it is also possible to configure this in the linux path `/etc/wpa_supplicant/wpa_supplicant.conf`). See below for example.
8. Connect the Pi using an ethernet cable and boot from the new SD card
9. Find the IP address of the Pi from the DHCP server
10. Log in to the terminal using SSH (user _pi_, password _raspberry_), eg: `ssh pi@192.168.0.123`
11. Check which wireless networks are visible: `sudo iwlist wlan0 scan | grep ESSID`
12. Edit the wireless config: `sudo nano /etc/wpa_supplicant/wpa_supplicant.conf`
13. Check if connected: `ifconfig wlan0`
14. Set a DHCP reservation for the MAC of the wireless adapter
15. Restart the adapter (`sudo ifdown wlan0 && sudo ifup wlan0`) or `pi sudo reboot`
16. Run `sudo raspi-config`, expand the filesystem and set internationalization options

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

If the Pi can't be found on the network connect it using the ethernet port. If found that way SSH in to it, then:

1. Check which wireless networks are visible: `sudo iwlist wlan0 scan | grep ESSID`
2. Edit the wireless config: `sudo nano /etc/wpa_supplicant/wpa_supplicant.conf`

```
network={
    ssid="MyNetwork"
    psk="s00perS3cure"
}
```

3. Check if connected: `ifconfig wlan0`

Once it's on the network you may want to:

1. Set a DHCP reservation for the MAC of the wireless adapter
2. Restart the adapter (`sudo ifdown wlan0 && sudo ifup wlan0`) or `pi sudo reboot`
3. Run `sudo raspi-config` and expand the filesystem
