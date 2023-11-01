---
title: 2023 HuntressCTF - Wimble
date: 2023-10-06T15:04:11-06:00
tags:
  - wim
  - wimtools
  - prefetch
image: /2023-HuntressCTF/wimble.png
---

### Summary
```
Author: @JohnHammond

"Gretchen, stop trying to make fetch happen! It's not going to happen!" - Regina George, Mean Girls

```

### Steps

I downloaded wimble.7z to my Kali VM and executed `7za e wimble.7z`.  I was presented with a file called fetch.  I executed `file fetch` and was given this result: ```fetch: Windows imaging (WIM) image v1.13, XPRESS compressed, reparse point fixup```.  I researched mounting .wim files on Linux and found `wimmount` from `wimtools` will mount the fetch file.  I created a new folder called `./mount` and ran this command the mount the file: `wimmount fetch ./mount`.  Next, I looked in the ./mount/ direcotry and discovered 276 .pf files.  

At this point, I decoded to move to Windows and see if I can use [Eric Zimmerman's PECmd Tool](https://f001.backblazeb2.com/file/EricZimmermanTools/PECmd.zip).  Since I already mounted the files on Linux, I decided to copy and paste the .pf files over to Windows. 

I used PECmd.exe to scan the direcotry where I put the prefetch files. 
```powershell
.\PECmd.exe -d "C:\Users\User\Downloads\wimble\mount" > results.txt
```

Instead of manually looking through the files, I wanted to see if the flag was in plaintext.  
```powershell
 $flag = Get-Content .\results.txt
 $flag | Select-String "flag"
 ```

 Running this command, I discovered the Flag: ```FLAG{97F33C9783C21DF85D79D613B0B258BD}```

![](/2023-HuntressCTF/wimble2.png)


