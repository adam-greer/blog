---
title: 2024 HuntressCTF - Myster
date: 2024-10-08T07:00:00-07:00
tags:
  - 
image: /2024-HuntressCTF/mystery.png
---

### Summary
```
Author: Michael Orlino

Someone sent this to me...
such enigma, such mystery:

rkenr wozec gtrfl obbur bfgma fkgyq ctkvq zeucz hlvwx yyzat zbvns kgyyd sthmi vsifc ovexl zzdqv slyir nwqoj igxuu kdqgr fdbbd njppc mujyy wwcoy

Settings as below:
3 Rotor Model
Rotor 1: VI, Initial: A, Ring A
Rotor 2: I, Initial: Q, Ring A
Rotor 3: III, Initial L, Ring A
Reflector: UKW B
Plugboard: BQ CR DI EJ KW MT OS PX UZ GH
```

### Steps

This was a new challenge. I started by googling `enigma cipher` and discovered [Enigma-Machine]("https://cryptii.com/pipes/enigma-machine").  I pasted in the cipher text and mirrored the settings within the challenge and got this response:

![](/static/2024-HuntressCTF/e1.png)

I can see the text has odd spacing, so I cleaned up the formatting and have this result:
```
message wrapped in light hidden deeper out of sight locking it more tight any way your flag is here flag fdfea bcacbebfbadaefbeccaadddbafezzz
```
After some quick trial and error I found the flag as: `flag{fdfeabcacbebfbadaefbeccaadddbafe}`


Flag: flag{fdfeabcacbebfbadaefbeccaadddbafe}