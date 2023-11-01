---
title: 2023 HuntressCTF - Layered Security
date: 2023-11-01T07:00:00-07:00
tags:
  - Steganography
image: /2023-HuntressCTF/ls.png
---

### Summary
```
Author: @JohnHammond  
  
It takes a team to do security right, so we have layered our defenses!
```

### Steps

After downloading ```Layered_security``` I executed ```file layered_security``` and observed the file is ```GIMP XCF image data```.  Next, I launched ```gimp layered_security``` to open the file in GIMP.  Initially, I see a photo with multiple layers. 

![](/2023-HuntressCTF/lsgimp.png)


Starting at the top layer, I removed each layer one at a time until getting to ```Pasted Layer $3``` where I found the flag. 

![](/2023-HuntressCTF/lsflag.png)

flag: ```flag{9a64bc4a390cb0ce31452820ee562c34}```
