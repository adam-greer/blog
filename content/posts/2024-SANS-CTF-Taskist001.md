---
title: 2024 SANS Offensive Operation CTF - Taskist 001
date: 2024-02-28T07:00:00-07:00
tags:
  - javascript
image: 
---


### Summary
```
We are working on this amazing new task manager app called Taskist Pro. Our devs claim the app is secure, we want you to take a look at it and see if you can leak the flag hidden inside the admin account.
```

### Taskist 001

I navigated to the site `http://taskist.pwn.site:1337/` and registered my own account.  I navigated to each area of the application and created a new task.  After reviewing the history in the proxy I noticed when a user navigates to the `/dashboard` endpoint, here is an api call to `/api/tasks/{userid}`.  This call will load the respected users tasks.  I tried manually adjusting this to `/api/tasks/1` assuming the admin was the 1st account, but no tasks were loaded.  I next, performed a small brute force fuzzing for userids 1-100 and found that the admin account was actually userid 64.  Here I was able to see a flag.

![](/2024/sansctf/taskist001.png)






