---
layout: post
title: Raspberry Pi Tweaks
tags:
  - raspberrypi
  - raspbian
  - tweaks
---

# Raspberry Pi Tweaks

## Disable HDMI Output

```
/usr/bin/tvservice -o
```

Add this line to `/etc/rc.local` to enable on startup.

Run `/usr/bin/tvservice -p` to turn it back on.

## Disable LEDs

https://www.jeffgeerling.com/blogs/jeff-geerling/controlling-pwr-act-leds-raspberry-pi

**Pi Zero**

```
# Disable the ACT LED on the Pi Zero.
dtparam=act_led_trigger=none
dtparam=act_led_activelow=on
```
**All Other Pis**

```
# Disable the ACT LED.
dtparam=act_led_trigger=none
dtparam=act_led_activelow=off

# Disable the PWR LED.
dtparam=pwr_led_trigger=none
dtparam=pwr_led_activelow=off
```

## Disable USB Ports

```
echo 0x0 > /sys/devices/platform/soc/3f980000.usb/buspower
```

Add this line to `/etc/rc.local` to enable on startup.

Run `echo 0x1 > /sys/devices/platform/soc/3f980000.usb/buspower` to turn it back on.
