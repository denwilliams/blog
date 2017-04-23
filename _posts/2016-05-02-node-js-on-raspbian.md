---
layout: post
title: Node JS on Raspbian (Raspberry Pi)
tags:
  - raspberrypi
  - raspbian
---

The following works on [Raspbian Jessie...](https://www.raspberrypi.org/downloads/raspbian/)

Install Node JS 6:

```
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Install the Node JS build tools if required:

```
sudo apt-get install -y build-essential
```

Check it's working:

```
node -v
npm -v
```

### Update

Apparently this only works for ARMv7 and later processors, so this doesn't work on Raspberry Pi first generations.

More info on Node installation for Pis here: https://github.com/nfarina/homebridge/wiki/Running-HomeBridge-on-a-Raspberry-Pi#install-node