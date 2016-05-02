---
layout: post
title: Getting Flic Buttons Running on the Raspberry Pi 3
tags:
  - raspberrypi
  - raspbian
  - flic
---

The official docs (https://github.com/50ButtonsEach/fliclib-linux-dist) were definitely missing a lot!

I had to `apt-get` install more than was suggested:

```
sudo apt-get install git libglib2.0-0 libglib2.0-dev libdbus-1-dev libudev-dev automake libtool libical-dev libreadline-dev libjson-glib-1.0-0 sudo apt-get install libsoup2.4-1
```

Building BlueZ worked as expected:

```
git clone git://git.kernel.org/pub/scm/bluetooth/bluez.git
cd bluez
git checkout 5.37
./bootstrap
./configure --enable-experimental --enable-library
make
sudo make install
```

I had to bring up the bluetooth controller with:

```
sudo hciconfig hci0 up
```

Then I was able to run everything in 3 terminals:

```
sudo ~/bluez/src/bluetoothd -nEd
sudo ~/flic/armv7l/daemon -l -f flic.sqlite3
sudo ~/flic/armv7l/fliclib-cpp/flic
```

Bluetoothd started automatically next reboot. To enable experimental (required for `daemon` to work):

```
sudo nano /lib/systemd/system/bluetooth.service
```

Then add ` -E` to the end of `ExecStart`

I was also able to get button presses registering using a simple Node script:

```
var flic = require('node-flic-buttons');
var buttons = new flic();
buttons.on('click', function (clickEvt) {
  console.log(clickEvt);
});
```

Output:
```
connected
{ deviceId: '80:E4:DA:xx:xx:xx',
  queued: false,
  timeDiff: 0,
  isSingleClick: true,
  isDoubleClick: false,
  isHold: false }
{ deviceId: '80:E4:DA:xx:xx:xx',
  queued: false,
  timeDiff: 0,
  isSingleClick: false,
  isDoubleClick: true,
  isHold: false }
```
