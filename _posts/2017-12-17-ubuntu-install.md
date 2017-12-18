---
layout: post
title: How install deb file in ubuntu 
---

### Why to use sudo apt-get install -f after sudo dpkg -i /path/to/deb/file


```
 -f, --fix-broken
           Fix; attempt to correct a system with broken dependencies in place.
```

```
$ sudo dpkg -i ./some.deb
$ sudo apt-get install -f

```
