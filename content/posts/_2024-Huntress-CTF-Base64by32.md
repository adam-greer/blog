---
title: 2024 HuntressCTF - Base64by32
date: 2024-10-01T07:00:00-07:00
tags:
  - 
image: /2024-HuntressCTF/base64by32.png
---

### Summary
```
Author: @JohnHammond

This is a dumb challenge. I'm sorry.
```

### Steps

I downloaded the challenge file to kali quickly noticed the text is more likely encoded with base64.  

```    
Vm0wd2QyUXlVWGxWV0d4V1YwZDRWMVl3WkRSV01WbDNXa1JTVjAxV2JETlhhMUpUVmpBeFYySkVU
bGhoTVVwVVZtcEJlRll5U2tWVQpiR2hvVFZWd1ZWWnRjRUpsUmxsNVUydFdWUXBpUjJodlZGWldk
MVpXV25SalJVcHNVbXhzTlZVeWRGZFdVWEJwVWpKb2RsWkdXbGRrCk1WcFhWMjVTYWxKVmNITlZi
WGh6VGxaVmVXUkdaRmRWV0VKd1ZXcEtiMlJzV2tkWGJHUnJDazFXY0ZoV01qVlRZV3hLVm1OSVRs
WmkKV0doNlZHeGFWbVZYVWtkYVJtUldWMFZLZDFaWGNFdGlNbEp6VjJ0a1dHSkhVbkpEYXpGWFkw
Wm9WMDFxVmxSWlYzaExWbTFPU1ZScwpXbWtLVjBkb05sWkhlR0ZXYlZaWVZXdGtZVkp0VWxkV01G
....
```

Using `cat base64by32 | base64 -d ` I see another base64 result.  Next I executed `cat base64by32 | base64 -d | wc -l` and see a result of `6310`.  Doing that again, by running `cat base64by32 | base64 -d | base64 -d wc -l` the result continues to get smaller.  This time the I see 4671. At this point, I believe the flag was base64 encoded 32 times.  To find the flag, I used the below:
```bash
for i in {1..32}; do
    cat base64by32 | tr -d "\n" | base64 -d > temp && mv temp base64by32
done
cat base64by32
```

Flag: flag{8b3980f3d33f2ad2f531f5365d0e3970}

