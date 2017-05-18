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

Apparently this only works for ARMv7 and later processors, so this doesn't work on Raspberry Pi first generations and Zeros.

To install on these, first get the URL to the version you want from https://nodejs.org/dist/ (Latest is always https://nodejs.org/dist/latest/).

Download and extract the package, eg:

```
wget https://nodejs.org/dist/latest/node-v7.10.0-linux-armv6l.tar.xz
tar -xJf node-v7.10.0-linux-armv6l.tar.xz
cd node-v7.10.0-linux-armv6l
```

Copy the files to `/usr/local`:

```
sudo cp -R * /usr/local/
```

`/usr/local/bin` should already be in the path so it should just work.

```
node -v
npm -v
```
