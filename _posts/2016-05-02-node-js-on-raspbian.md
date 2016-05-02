---
layout: post
title: Node JS on Raspbian (Raspberry Pi)
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
