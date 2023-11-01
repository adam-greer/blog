---
title: 2023 HuntressCTF - Snake Eater
date: 2023-11-01T07:00:00-07:00
tags:
  - Malware
  - Reverse Enginering
  - RE
image: /2023-HuntressCTF/snakeeater.png
---

### Summary
```
Author: @HuskyHacks

Hey Analyst, I've never seen an executable icon that looks like this. I don't like things I'm not familiar with. Can you check it out and see what it's doing?

```

### Steps

I started up my Windows 11 VM  with Flare installed.  I began by disabling my network connectivity, USB controller, and shared files and folders.  Once the VM was ready, I executed the binary and didn't see any response or indication on the OS.  
![](/2023-HuntressCTF/se1.png)

Before starting IDA, I wanted to try a few things. I tried to see if there was a help menu and to my surpise there was.

![](/2023-HuntressCTF/se2.png)

Using the information provided to me, I executed the binary with the ```-v``` flag.

![](/2023-HuntressCTF/se3.png)

I worked on this for a big longer but after a period of time I didn't get anywhere.  This time I decided to use ProcMon to see what was happening on the OS.  I know ProcMon is going to generate alot of information, so I decided to create an Include filter to only display events by snake_eater.exe. 

![](/2023-HuntressCTF/se4.png)

I navigated back to cmd prompt and executed snake_eater.exe continuing to use --verbose mode.

![](/2023-HuntressCTF/se5.png)

I stopped capturing after events stopping reporting in the application.  Before going line-by-line, I wanted to get an overview of what was happening with an easier glance by looking at all the file events, network events, and registry events.  In ProcMon, I went to Tools -> File Summary... and to my surprise, the application was writing out the flag within the ApPData Roaming folder!

Flag: ```flag{d1343a2fc5d8427801dd1fd417f12628}```

![](/2023-HuntressCTF/seflag.png)
