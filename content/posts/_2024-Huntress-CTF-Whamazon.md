---
title: 2024 HuntressCTF - Whamazon
date: 2024-10-04T07:00:00-07:00
tags:
  - 
image: /2024-HuntressCTF/whamazon.png
---

### Summary
```
Author: @JohnHammond

Wham! Bam! Amazon is entering the hacking business! Can you buy a flag?
```

### Steps

I started the docker instance and navigated to the challenge and was presented with this game.

![](/static/2024-HuntressCTF/w1.png)


Selecting 1, I see there's nothing in my inventory. 

![](/static/2024-HuntressCTF/w2.png)

Going to the option to buy items, I see I can buy various items including a flag.  However, the flag costs 1000000000, and I have 50 available to me.  I went to purchase some apples and see each apple is 3 dollars.  I purchased 3 apples at 3 dollars which removed 9 dollars from my account. I went back to purchase some more apples, but this time I put in `-100000000000000`.  The way the game is calculating the purchase, it actually allow negative numbers which result in a positive dollar amount. 

![](/static/2024-HuntressCTF/w3.png)

With enough money in my wallet, I go back and purchase the flag, but not before a quick round of rock, paper, scissors. 

![](/static/2024-HuntressCTF/w4.png)

Flag: flag{18bdd83cee5690321bb14c70465d3408}