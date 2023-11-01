---
title: 2023 HuntressCTF - Comprezz
date: 2023-11-01T07:00:00-07:00
tags:
  - 
image: /2023-HuntressCTF/comprezz.png
---

### Summary
```
Author: @JohnHammond

Someone stole my S's and replaced them with Z's! Have you ever seen this kind of file before?
```

### Steps

After downloading ```comprezz``` to my Kali instance, I ran ```file comprezz``` an d received the following output ```��f؄9�'FnĠ���j�CC�34h̐q���f0Z�%```  Based on the challenge name and that the file is not readable, I decided to try to uncompress the file using. First I changed the file name from ```comprezz``` to ```comprezz.z```  Then I used ```uncompress comprezz```.   The extract file is comprezz which had the flag.

```bash
flag{196a71490b7b55c42bf443274f9ff42b}
```
