---
title: 2023 HuntressCTF - Rock, Paper, Psychic
date: 2023-10-06T15:04:11-06:00
tags:
  - ReverseEngineering
  - RE
  - Ghidra
image: /2023-HuntressCTF/rpp.png
---

### Summary
```
Author: @HuskyHacks

Wanna play a game of rock, paper, scissors against a computer that can read your mind? Sounds fun, right?

```

### Steps

I downloaded the executible to my Flare Windows VM and executed it.  I was presented with a game of rock, paper, scissors. 

![](/2023-HuntressCTF/rpp1.png)

Unfortuntally, reverse enginnering is not something i'm very skilled at and this challenge took me a while to figure out exactly what was going on.  To start the RE process, I figured up Ghidra and loaded the file.  I let Ghidra auto analyze the file and I started to look through the Imports, Exports and functions.   I discovered the ```playerWins__main_10``` function. 

![](/2023-HuntressCTF/rpp2.png)

I navigated to the XREF to see where this function would be called from and I see there is an instruction `JNZ`.  Here the function would not be called and skipped over since the condition was not met.  I changed the instruction to `JZ`. 

![](/2023-HuntressCTF/rpp3.png)

Lastly, I exported the program as `rock_paper_psychic-new.exe` and ran it again and got the flag: ```flag{35bed450ed9ac9fcb3f5f8d547873be9}```

![](/2023-HuntressCTF/rpp4.png)

```
Special Thanks to Talnet23 to providing guidance on this challenge
```



