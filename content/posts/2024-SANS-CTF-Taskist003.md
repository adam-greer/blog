2---
title: 2024 SANS Offensive Operation CTF - Taskist 003
date: 2024-02-28T07:00:00-07:00
tags:
  - javascript
image: 
---


### Summary
```
Wow! You compromised the admin account! Looks like there's some interesting information on the admin dashboard and some additional features, can you read the application's server-side source code?
```

### Taskist 003

While logged into the application as an admin, I now had access to the site_configuration where we can import and export configuration setting.  I first exported the current site configuration and then re-imported it to understand the format that was required to import. After a few minutes, I discovered the `site_logo` is vulnerable to Server Side Request Forgery (SSRF) through the file schema. I was able to confirm this by obtaining the `/etc/passwd` file. 

![](/2024sansctf/taskist003.png)

Initially, this SSRF was limited to just local file reads so there was a fair amount of guess work involved trying to figure out the right file names.  Additionally, I was provided a clue that the app was still located in the `/app` directory. From the Admin's task list.  Eventually, I was able to locate `/app/index.js` which had the flag.

![](/2024sansctf/taskist003-2.png)











