---
title: 2023 HuntressCTF - BaseFFFF+1
date: 2023-11-01T07:00:00-07:00
tags:
  - base65536
image: /2023-HuntressCTF/base.png
---

### Summary
```
Author: @JohnHammond

Maybe you already know about base64, but what if we took it up a notch?
```

### Steps

To start this challenge I ran `file` against the basefff1 file and see that its is `baseffff1: Unicode text, UTF-8 text, with no line terminators`.  Next, previewing the file I see these characters:

![](/2023-HuntressCTF/base1.png)

After many failed decoding attempts, I went back to the challenge description and started to work on what `FFFF+1` means.  Eventually, I found that FFFF is a hex value for 65535. Here is the recipe in [CyberChef](https://gchq.github.io/CyberChef/#recipe=From_Base(16)To_Base(10)&input=RkZGRg) 

![](/2023-HuntressCTF/base2.png)

Next, `FFFF+1` or `65535+1` would be `65536`.  Looking back at the challenge name, it would be renamed to `Base65536`.  Looking online I found CyberChef doesn't have this option yet, but I was able to locate [Base65536 Encoder/Decoder](https://www.better-converter.com/Encoders-Decoders/Base65536-Decode). 

Using this tool, I was able to decode the flag: ```flag{716abce880f09b7cdc7938eddf273648}```

![](/2023-HuntressCTF/base3.png)