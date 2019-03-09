---
layout: post
title: Autostarting PM2 on Raspbian
tags:
  - raspberrypi
  - raspbian
  - pm2
---

This seemed to be the best way to get it to work:

```
sudo env PATH=$PATH:/usr/local/bin pm2 startup systemd -u pi --hp /home/pi
```

Then use `pm2 start...` to add any services to autostart, then `pm2 save` to remember the currently running instances on reboot.
