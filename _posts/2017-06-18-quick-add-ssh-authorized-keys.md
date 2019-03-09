---
layout: post
title: Quickly adding SSH public key to Authorized Hosts
tags:
  - linux
  - ssh
---

# Quickly adding SSH public key to Authorized Hosts

```
cat ~/.ssh/id_rsa.pub | ssh USER@HOST "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```
