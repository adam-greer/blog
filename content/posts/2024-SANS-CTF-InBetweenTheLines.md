---
title: 2024 SANS Offensive Operation CTF - In Between The Lines 001-002
date: 2024-02-28T07:00:00-07:00
tags:
  - gif
  - convert
image: 
---

### Summary
```
Hey check out this awesome gif I found!
```

### Steps

The gif file has one image that contains a flag near the top right corner, but as you see its quite difficult to see without modification. 

![](/2024sansctf/ibtl001.gif)

I used the utility covert from ImageMagick to expand the gif into individual images.  I used the following syntax to achieve this.

```bash
convert chall.gif chall.png
```

Now, I had multiple chall.png files for each frame of the gif.  

![](/2024sansctf/ibtl001-2.png)

For In Between The Lines 002, there is another gif file that shows part of the flag in each frame as seen below.

![](/2024sansctf/ibtl002.gif)

I used the same technique to convert the files into individual files and then manually typed the flag.

![](/2024sansctf/ibtl002-2.png)

The final result was: `flag{W31c0M3_70_7H3_111_80X_0F_Ur_UN1M461N4813_P41N_4150_15N7_U51N6_4_0Cr_50_C001_11K3_17_15_U53FU1}`