---
layout: post
title: Installing Grafana on a Raspberry Pi
tags:
  - linux
  - grafana
  - raspberrypi
---

> Help from: https://github.com/fg2it/grafana-on-raspberry/wiki

```
sudo apt-get install apt-transport-https curl
curl https://bintray.com/user/downloadSubjectPublicKey?username=bintray | sudo apt-key add -

echo "deb https://dl.bintray.com/fg2it/deb jessie main" | sudo tee -a /etc/apt/sources.list.d/grafana.list

sudo apt-get update
sudo apt-get install grafana
sudo service grafana-server start
```

