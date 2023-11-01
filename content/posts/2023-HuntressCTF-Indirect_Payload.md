---
title: 2023 HuntressCTF - Indirect Payload
date: 2023-11-01T07:00:00-07:00
tags:
  - web
image: /2023-HuntressCTF/ip.png
---

### Summary
```
Author: @JohnHammond

We saw this odd technique in a previous malware sample, where it would uncover it's next payload by... well, you'll see.

```

### Steps

I started the docker instance for this challenge and navigated to the website and am presented with a button to ```Retrieve the Payload```

![](/2023-HuntressCTF/ip2.png)

The web server generates 20 302 redirects and at this point the browser intrupts and stops redirecting and generates an error.

![](/2023-HuntressCTF/ip3.png)

Looking at the history in burp suite, I noticed that every other request had a MIME type of text.  Investgating the ```text MIME type``` I noticed that its hinting towards the flag.

![](/2023-HuntressCTF/ip4.png)

I changed the filter on BurpSuite to only display ```Other text```

![](/2023-HuntressCTF/ip5.png)

Since the browser stops redirecting after 20 requests, I looked at the last request and next manually navigated to that path. 

![](/2023-HuntressCTF/ip6.png)

As I expected, I started to get more redirects.  I continued to use ```Copy URL``` on the last request until I no longer received any more redirects and confirmed by finding the last ```}``` that indicates the last character of the flag.

![](/2023-HuntressCTF/ip7.png)

I manually assembeled the flag and received: ```flag{448c05ab3e3a7d68e3509eb85e87206f}```
