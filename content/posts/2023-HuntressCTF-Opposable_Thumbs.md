---
title: 2023 HuntressCTF - Opposable Thumbs
date: 2023-11-01T07:00:00-07:00
tags:
  - Forensics
  - Thumbnnails

image: /2023-HuntressCTF/ot.png
---

### Summary
```
Author: @JohnHammond

We uncovered a database. Perhaps the flag is right between your fingertips!

```

### Steps

This challenge started with a file called ```thumbcache_256.db```.  I initially started with my Linux VM, but soon discovered this file is part of the windows operating system and I found an open source project that allows us to extract the thumbnail images from the database file.  You can find more on the windows program [here](https://thumbcacheviewer.github.io/).  I pivoted over to my Windows Flare VM and installed this application and loaded the .db file.

This db file has 22 objects present and I found I could use ```CTRL + A``` to select all objects and right click and use ```Save Selected ``` and saved them to a new folder called ThumbNails.

![](/2023-HuntressCTF/ot1.png)

Only valid image files are extracted and I found the flag was the image of ```3fa8aafdd63e1168.jpg```

Flag: ```flag{human_after_all}```

![](/2023-HuntressCTF/ot2.png)


