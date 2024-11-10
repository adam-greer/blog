---
title: 2024 HuntressCTF - Keyboard Junkie
date: 2024-10-14T07:00:00-07:00
tags:
  - 
image: /2024-HuntressCTF/KeyboardJunkie.png
---

### Summary
```
Author: @JohnHammond

My friend wouldn't shut up about his new keyboard, so...
```

### Steps

This challenge was a pcap file however, of USB traffic not HTTP traffic as i'm use to. I discovered a utility on github call [ctf-usb-keyboard-parser](https://github.com/TeamRocketIst/ctf-usb-keyboard-parser)to convert the usb data into hex values.  I downloaded the file and followed the instructions. 

```bash
tshark -r ./usb.pcap -Y 'usb.capdata && usb.data_len == 8' -T fields -e usb.capdata | sed 's/../:&/g2'
```

Next, I used the usbkeyboard.py to extract the keyboard presses resulting in the following:
```bash
python3 ./usbkeyboard.py hexdata 
so the answer is flag{f7733e0093b7d281dd0a30fcf34a9634} hahahah lol
```

Flag: flag{f7733e0093b7d281dd0a30fcf34a9634}