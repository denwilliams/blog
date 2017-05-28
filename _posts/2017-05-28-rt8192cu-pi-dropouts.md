---
layout: post
title: Raspberry Pi Tweaks
tags:
  - raspberrypi
  - raspbian
  - wifi
  - dropouts
---

# Raspberry Pi WiFi Dropouts (rt8192cu)

Check which driver it is using:

```
readlink /sys/class/net/wlan0/device/driver
```

If it's `../../../../../../../../../bus/usb/drivers/rtl8192cu` then:

```
sudo nano /etc/modprobe.d/8192cu.conf
```

And set contents:

```
# Disable power saving
options 8192cu rtw_power_mgnt=0 rtw_enusbss=1 rtw_ips_mode=1
```
