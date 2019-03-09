---
layout: post
title: Getting Flic Buttons Running on the Raspberry Pi 3 - Take 2
tags:
  - raspberrypi
  - raspbian
  - flic
---

Clone it to the Pi:
```
sudo apt-get install git
cd /opt
sudo git clone https://github.com/50ButtonsEach/fliclib-linux-hci
```

Create the data folders:
```
sudo mkdir /var/lib/flic
```

Create a systemd start script:
```
sudo nano /etc/systemd/system/flicd.service
```

Contents:
```
[Unit]
Description=flicd Service
After=bluetooth.service
Requires=bluetooth.service

[Service]
TimeoutStartSec=0
ExecStart=/opt/fliclib-linux-hci/bin/armv6l/flicd -f /var/lib/flic/flic.db -s 0.0.0.0 -h hci0 -w -l /var/log/flic.log
Restart=always
RestartSec=3

[Install]
WantedBy=multi-user.target
```

...then...

```
sudo systemctl enable flicd
```


Restart.

Boom.
