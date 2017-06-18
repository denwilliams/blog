---
layout: post
title: Raspberry Pi Tweaks
tags:
  - linux
  - ssh
---

# Quickly adding SSH public key to Authorized Hosts

```
cat ~/.ssh/id_rsa.pub | ssh USER@HOST "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```
