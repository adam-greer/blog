---
title: 2024 HuntressCTF - Mimi
date: 2024-10-01T07:00:00-07:00
tags:
  - 
image: /2024-HuntressCTF/mimi.png
---

### Summary
```
Author: @JohnHammond

Uh oh! Mimi forgot her password for her Windows laptop!

Luckily, she dumped one of the crucial processes running on her computer (don't ask me why, okay)... can you help her recover her password?

NOTE: This file on its own is not malware per say, but it is likely to raise antivirus alerts. Would recommend examining this inside of a virtual environment.
```

### Steps

I downloaded the file and extracted it on my Linux system.  The first command I ran was `file mimi` and discovered this is a `Mini DuMP crash report, 18 streams, Tue Sep 10 02:33:22 2024, 0x461826 type`.  Based on the challenge description I had a feeling it was associated with Mimikatz.  I copied the file over to Windows, but had a hard time getting Mimiktaz to read the mimi file.  After a quick google search, I discovered `pypykatz` and found it was a linux based implementation.  A quick review of the the documentation I ran  `pypykatz lsa minidump mimi` and found this program would parse the dmp file and show the extracted mimikatz dump data.  This resulted in the flag as's Mimi's plain text  password.

![](/static/2024-HuntressCTF/mimi1.png)

Flag: flag{7a565a86761a2b89524bf7bb0d19bcea}