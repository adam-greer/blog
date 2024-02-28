2---
title: 2024 SANS Offensive Operation CTF - Taskist :: 002
date: 2024-02-28T07:00:00-07:00
tags:
  - javascript
image: 
---


### Summary
```
Great, you were able to leak sensitive information of the admin account! But can you log in as the admin account now? Play around with other features available on the platform!
```

### Taskist 002

While enumerating the application I found that you can change the userid when performing a password change. Using a proxy, I intercepted the password change request and changed it to the admin's userid of `64`, and we received the below responses.

![](/2024/sansctf/taskist002.png)

Next, I logged into the application with the username and password of `admin:br0k3n_p4ss__c0ntr0l_l0gin` and obtained the flag.

![](/2024/sansctf/taskist002-2.png)









