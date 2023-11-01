---
title: 2023 HuntressCTF - Babel
date: 2023-10-06T15:04:11-06:00
tags:
  - 
image: /2023-HuntressCTF/babel.png
---

### Summary
```
Author: @JohnHammond

It's babel! Just a bunch of gibberish, right?
```

### Steps

This challenge gives us a C++ source code file. Looking at the file the variable `pTIxJTjYJE` looks like it has a base64 encoded string.  This string alone cannot be decoded as its not a valid string.  The next part of the code defines a another variable `YKyumnAOcgLjvK` and this looks like its being used a key to replace characters from `pTIxJTjYJE` with characters from `YKyumnAOcgLjvK`.  
```bash
Assembly smlpjtpFegEH = Assembly.Load(Convert.FromBase64String(zcfZIEShfvKnnsZ(pTIxJTjYJE, YKyumnAOcgLjvK)));
```

This python script will perform the subsitition for me and create a valid base64 string.
```python
def perform_substitution(t, k):
    bnugMUJGJayaT = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ"
    WgUWdaUGBFwgN = ""

    OrnBLfjI = dict(zip(k, bnugMUJGJayaT))

    for char in t:
        if char.isalpha():
            if char.isupper():
                WgUWdaUGBFwgN += OrnBLfjI.get(char, char)
            else:
                WgUWdaUGBFwgN += OrnBLfjI.get(char.lower(), char)
        else:
            WgUWdaUGBFwgN += char

    return WgUWdaUGBFwgN

pTIxJTjYJE = "<base64string>"

YKyumnAOcgLjvK = "lQwSYRxgfBHqNucMsVonkpaTiteDhbXzLPyEWImKAdjZFCOvJGrU"

decoded_assembly_bytes = perform_substitution(pTIxJTjYJE, YKyumnAOcgLjvK)
print(decoded_assembly_bytes)
```

Next, I used CyberChef to perform the base64 decode and I see the header starts with MZ. 

![](/2023-HuntressCTF/babel1.png)


I downloaded the file to my VM and ran `strings` against the file, and found the flag: `flag{b6cfb6656ea0ac92849a06ead582456c}`

