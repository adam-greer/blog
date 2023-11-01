---
title: 2023 HuntressCTF - Traffic
date: 2023-11-01T07:00:00-07:00
tags:
  - forensics
  - zeek
image: /2023-HuntressCTF/traffic.png
---

### Summary
```
Author: @JohnHammond

We saw some communication to a sketchy site... here's an export of the network traffic. Can you track it down?

Some tools like rita or zeek might help dig through all of this data!
```

### Steps

After downloading ```traffic.7z``` to my Kali instance, I extracted the archive using ```7za e traffic.7z```.  Once extracted I observed various logs in .gz format.


![](/2023-HuntressCTF/zeeklogs.png)

I was already familiar with these logs from my time working with Bro in the past.  Based on the challenge description they already hinted at network traffic and observing a sketcy site. So I knew to go directly to the dns logs. 

I extracted the dns*.log.gz files using ```gunzip -d dns.*```.  Next, I used ```cat dns.*.log``` to start to get an idea what traffic was observed.  These five dns log files had ```17134``` lines. Instead of following the advice of description and installing zeek and or rita, I decided to grep my way through the results. 

To start with a fresh list of domains, I executed ```cat dns*.log | awk '{ print $10 }'``` to pull out just the domains and move those into a file called domains.txt

First, I wanted to match on a ```.``` to include the domains with a tld. Next, using grep's invert match, I started to eliminate legitimate domains.  Eventually I was able to narrow it down to ```1722```  domains using 

```bash
cat domains.txt | sort -u | grep '\.' | grep -v \.google\.com | grep -v \.local | grep -v \.yahoodns\.net | grep -v \.microsoft\. | grep -v \.amazonaws\. | grep -v \.akamaihd\. | grep -v yahoo\. 
``` 

Eventually I found ```sketchysite.github.io```<br>
![](/2023-HuntressCTF/sketchysite.png)

Navigating to this domain I discovered the flag!<br>
```flag{8626fe7dcd8d412a80d0b3f0e36afd4a}```

![](/2023-HuntressCTF/flag.png)
