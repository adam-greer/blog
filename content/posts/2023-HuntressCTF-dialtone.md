---
title: 2023 HuntressCTF - Dialtone
date: 2023-10-06T15:04:11-06:00
tags:
  - wav
  - bigint
image: /2023-HuntressCTF/dialtone.png
---

### Summary
```
Author: @JohnHammond#6971

Well would you listen to those notes, that must be some long phone number or something!

```

### Steps

In this challenge I was given a file called ```dialtone.wav```.  Listening, I hear the audible dial pad when dialing a phone number.  After some research, I discoverd a github respository by [ribt](https://github.com/ribt/dtmf-decoder) that will convert a .wav file dial press and corrolate this with the actual number being dialed. I executed ```./dtmf.py ~/huntress/dialtone.wav``` and received the below response. 
```
13040004482820197714705083053746380382743933853520408575731743622366387462228661894777288573
```

I spent a bit of time trying to figure this value including going through the various operations on CyberChef.  Eventually, I discovered [Dencode](https://dencode.com/en/).  This website will encode and decode a string in various formats.  With trial and error I discovered the website performed a Num to Hex encoding and gave me this string: ```666c61677b36633733336566303962633466326134333133666636333038376532356436377d```.  Moving back to CyberChef, I decoded this value from Hex and got the flag!
flag: ```flag{6c733ef09bc4f2a4313ff63087e25d67}```