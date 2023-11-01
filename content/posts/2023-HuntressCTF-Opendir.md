---
title: 2023 HuntressCTF - Opendir
date: 2023-11-01T07:00:00-07:00
tags:
  - Malware
  - web
image: /2023-HuntressCTF/opendir.png
---

### Summary
```
Author: @JohnHammond

A threat actor exposed an open directory on the public internet! We could explore their tools for some further intelligence. Can you find a flag they might be hiding?

NOTE: This showcases genuine malware samples found a real opendir. For domain reputation purposes, this is behind Basic Authentication with credentials: opendir:opendir

```

### Steps

After authenticating to the application, i'm presented with a directory listing of the web server.  I navigated to each of the files that were .cmd, .bat, .txt, etc.  After a few minutes of browsing I discovered ```http://chal.ctf.games:31439/sir/64_bit_new/oui.txt``` and about half way down the page, I discovered the flag. 

![](/2023-HuntressCTF/opendirflag.png)


flag: ```flag{9eb4ebf423b4e5b2a88aa92b0578cbd9}```
