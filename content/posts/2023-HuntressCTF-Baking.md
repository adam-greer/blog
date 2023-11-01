---
title: 2023 HuntressCTF - Baking
date: 2023-11-01T07:00:00-07:00
tags:
  - web
  - cookies
image: /2023-HuntressCTF/baking.png
---

### Summary
```
Author: @JohnHammond

Do you know how to make cookies? How about HTTP flavored?

```

### Steps

I started the challenge docker instance and navigated to the url.  I'm presented with a six functions on the website that will "bake" within a given period of time. 

![](/2023-HuntressCTF/ezbakeoven.png)

When clicking on the cook function a POST request is sent for the corrosponding recipe and the timer starts on the oven. 

![](/2023-HuntressCTF/muffins.png)

on the POST request, I noticed the Cookie value is base63 encoded and the decoded value includes the recipe and time.  

![](/2023-HuntressCTF/time.png)

Looking at the ```Magic Cookies```, I see it will take 7200 minutes to bake.  Using BurpSuite, I set the proxy Intercept to on, and clicked on Cook for ```Magic Cooies```

![](/2023-HuntressCTF/burp1.png)

I copied the Cookie value over to decoder and changed the daate from 10/16/2023 to 10/6/2023 and encoded the new value as base64.

![](/2023-HuntressCTF/timechange.png)

Next, I copied the new base64 cookie value and navigated back o the Proxy tab and replaced the old cookie value with the new one and forwarded the request. 

![](/2023-HuntressCTF/ezbakeovenflag.png)

flag: ``` flag{c36fb6ebdbc2c44e6198bf4154d94ed4}```