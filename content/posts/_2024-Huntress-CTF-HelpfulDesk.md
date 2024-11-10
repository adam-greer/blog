---
title: 2024 HuntressCTF - HelpfulDesk
date: 2024-10-21T07:00:00-07:00
tags:
  - 
image: /2024-HuntressCTF/h1.png
---

### Summary
```
Author: @HuskyHacks

HelpfulDesk is the go-to solution for small and medium businesses who need remote monitoring and management. Last night, HelpfulDesk released a security bulletin urging everyone to patch to the latest patch level. They were scarce on the details, but I bet that can't be good...
```

### Steps


I started the docker instance and noticed that the current version is running 1.1. 
![](/static/2024-HuntressCTF/h2.png)

Navigating to the Security Update Required page, I can download the source code for version 1.1 and version 1.2.  I started with version 1.1 and loaded HelpfulDesk.dll into dnspy. 

I found that were are multiple paths disclosed within the .dll. 

![](/static/2024-HuntressCTF/h3.png)

I manually navigated to the paths I see there was a lack of access control on `/Setup/SetupComplete/` and `/Setup/SetupWizard/`.

Looking at `/Setup/SetupWizard/`, this looks like a page to setup the administrator username and password for the application.  

![](/static/2024-HuntressCTF/h4.png)

I input `admin:admin` and tested if it would work, and to my surprise it performed a 302 redirect back to the main page to login page where I can now login with those credentials. 

![](/static/2024-HuntressCTF/h5.png)

When a client is online, we can use this application to browse the files on the various systems. The first system, I looked at was `HOST-WIN-DX130S2` which had the flag.txt on the Desktop.

![](/static/2024-HuntressCTF/h5.png)


Flag: flag{03a6f458b7483e93c37bd94b6dda462b}