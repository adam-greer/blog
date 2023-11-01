---
title: 2023 HuntressCTF - Query Code
date: 2023-11-01T07:00:00-07:00
tags:
  - 
image: /2023HuntressCTF-Traffic/querycode.png
---

### Summary
```
Author: @JohnHammond

What's this?

```

### Steps

I downloaded the ```query_code``` file and executed ```file query_code``` and received the following response 
```bash
query_code: PNG image data, 111 x 111, 1-bit colormap, non-interlaced
```

Naming the file to query_code.png, I opened the file in FireFox to see a QR code.

![](/2023-HuntressCTF/qrcode.png)

I opted to use scanqr.org to read the response of the QR code and I discovered the flag.

![](/2023-HuntressCTF/querycodeflag.png)

flag: ```flag{3434cf5dc6a865657ea1ec1cb675ce3b}```