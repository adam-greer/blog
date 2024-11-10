---
title: 2024 HuntressCTF - Typo
date: 2024-10-11T07:00:00-07:00
tags:
  - 
image: /2024-HuntressCTF/typo.png
---

### Summary
```
Author: @JohnHammond

Gosh darnit, I keep entering a typo in my Linux command prompt!
```

### Steps

When starting the challenge, I was provided the following information:

```
# Password is "userpass"
ssh -p 32279 user@challenge.ctf.games
```

Upon logging in, I was presented with the below animation and then the connection closed. 

![](/static/2024-HuntressCTF/train.gif)

I was  unsuccessful in finding a way to interrupt the animation. However, after messing around with SSH, I found I would append commands to back the ssh command such as: `ssh user@challenge.ctf.games -p 32279 'ls'`.  This resulted in showing the flag.txt in the /home directory. Next, I used `ssh user@challenge.ctf.games -p 32279 'cat flag.txt'` to read the flag.txt file.



Flag: flag{36a0354fbf59df454596660742bf09eb}