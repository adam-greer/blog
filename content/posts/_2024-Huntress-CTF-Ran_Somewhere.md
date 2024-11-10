---
title: 2024 HuntressCTF - Ran Somewhere
date: 2024-10-08T07:00:00-07:00
tags:
  - 
image: /2024-HuntressCTF/rs.png
---

### Summary
```
Author: @Spyderwall

Thanks for joining the help desk! Here's your first ticket of the day; can you help the client out?
```

### Steps

This challenge had an .eml file with three attachments.  Starting off with the email I was presented with this information.

![](/static/2024-HuntressCTF/rs2.png)

The URL in the signature was point to `https://sites.google.com/view/id-10-t/home`. 

Moving on to look at the attachments, I see `4e 6f 74 65.txt` which translates to `note.txt` and the file was a hex encoded message.

```
48 65 79 20 54 68 65 72 65 21 20 59 6f 75 20 73 68 6f 75 6c 64 20 62 65 20 6d 6f 72 65 20 63 61 72 65 66 75 6c 20 6e 65 78 74 20 74 69 6d 65 20 61 6e 64 20 6e 6f 74 20 6c 65 61 76 65 20 79 6f 75 72 20 63 6f 6d 70 75 74 65 72 20 75 6e 6c 6f 63 6b 65 64 20 61 6e 64 20 75 6e 61 74 74 65 6e 64 65 64 21 20 59 6f 75 20 6e 65 76 65 72 20 6b 6e 6f 77 20 77 68 61 74 20 6d 69 67 68 74 20 68 61 70 70 65 6e 2e 20 57 65 6c 6c 20 69 6e 20 74 68 69 73 20 63 61 73 65 2c 20 79 6f 75 20 6c 6f 73 74 20 79 6f 75 72 20 66 6c 61 73 68 20 64 72 69 76 65 2e 20 44 6f 6e 27 74 20 77 6f 72 72 79 2c 20 49 20 77 69 6c 6c 20 6b 65 65 70 20 69 74 20 73 61 66 65 20 61 6e 64 20 73 6f 75 6e 64 2e 20 41 63 74 75 61 6c 6c 79 20 79 6f 75 20 63 6f 75 6c 64 20 73 61 79 20 69 74 20 69 73 20 6e 6f 77 20 27 66 6f 72 74 69 66 69 65 64 27 2e 20 59 6f 75 20 63 61 6e 20 63 6f 6d 65 20 72 65 74 72 69 65 76 65 20 69 74 2c 20 62 75 74 20 79 6f 75 20 67 6f 74 20 74 6f 20 66 69 6e 64 20 69 74 2e 20 49 20 6c 65 66 74 20 61 20 63 6f 75 70 6c 65 20 6f 66 20 66 69 6c 65 73 20 74 68 61 74 20 73 68 6f 75 6c 64 20 68 65 6c 70 2e 0a 2d 20 56 69 67 69 6c 20 41 6e 74 65
```

```
Hey There! You should be more careful next time and not leave your computer unlocked and unattended! You never know what might happen. Well in this case, you lost your flash drive. Don't worry, I will keep it safe and sound. Actually you could say it is now 'fortified'. You can come retrieve it, but you got to find it. I left a couple of files that should help.
- Vigil Ante
```

The other two .dat files were actually images. `66 69 6e 64 20 69 74 20 79 65 74.dat` is `find it yet.dat` and the last one `69 6d 20 6e 65 61 72 62 79.dat` is `im nearby.dat`.  Renaming each of the files to a .png, I observed the photos were taken near some type of structure that was similar to a castle. 

![](/static/2024-HuntressCTF/rs3.png)

![](/static/2024-HuntressCTF/rs4.png)

Going back to the email, we know the Mack was a clients coffee shop when his USB was stolen. Navigating to the website, I found a testimonial from Z Vault Coffee Shop, expressing the frustration with with D10T solutions.  L

![](/static/2024-HuntressCTF/rs5.png)


Looking at Google, I see that Z Vault Cafe is set to close and they are in Bel Air Maryland. 

![](/static/2024-HuntressCTF/rs6.png)

I used the search query `Del Air Md Castle` in Google, and stumbled upon `theknot.com` which had the Bel Air Armory which ended up being the solution.


![](/static/2024-HuntressCTF/rs7.png)


