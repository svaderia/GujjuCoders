---
layout: post
title: Overcome apt lock
author: sam
category: Notes
tags: [ubuntu]
image: /assets/linux.png
---

Many a time while using 
```bash
sudo apt-get update
``` 
we find a error staring back 
```bash
E: Could not get lock /var/lib/apt/lists/lock - open (11: Resource temporarily unavailable)
E: Unable to lock directory /var/lib/apt/lists/
``` 
There is a way to skip or overcome this without a reboot.

Mostly the solution recommend deleting the lock. I don't recommend doing that as a first measure; maybe if there is no alternative. The lock is placed when an apt process is running, and is removed when the process completes. If there is a lock with no apparent process running, this may mean the process got stuck for some reason.

If you try
```bash
ps aux | grep apt
```
that will catch processes containing the word apt, at least. If you see an apt-get process or an aptitude process that looks stuck, you can try
```bash
kill processnumber
```
and if that doesn't work try
```bash
kill -9 processnumber
```
This should kill the process and may remove the lock. Killing an apt or aptitude process is harmless unless it is actually in the middle of package installation. In any case, if the process got stuck, you probably don't have a choice but to kill it.

Killing a dpkg process directly, if present, is not a good idea, because if dpkg is active, it is probably manipulating the package database, and killing it may leave the package database in an inconsistent state; i.e. corrupted.

Killing an apt-get or aptitude process is in general much safer.