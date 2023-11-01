---
title: 2023 HuntressCTF - Land Before Time
date: 2023-11-01T07:00:00-07:00
tags:
  - Steganography
  - iSteg
image: /2023-HuntressCTF/landbeforetime.png
---

### Summary
```
Author: @proslasher

This trick is nothing new, you know what to do: iSteg. Look for the tail that's older than time, this Spike, you shouldn't climb.
```

### Steps

The challenge description gave us a hint by calling for iSteg. Looking on Github I discovered [iSteg by rafiibrahim8](https://github.com/rafiibrahim8/iSteg).  I downloaded the the jar file to Kali and executed it using ```java -jar iSteg-v2.1_GUI.jar```.  This launched the GUI and I was able to reveal the hidden text and get the flag. 

![](/2023-HuntressCTF/landbeforetimeflag.png)

flag: flag{da1e2bf9951c9eb1c33b1d2008064fee}