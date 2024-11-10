---
title: 2024 HuntressCTF - GoCracKMe1
date: 2024-10-09T07:00:00-07:00
tags:
  - 
image: /2024-HuntressCTF/gcm1.png
---

### Summary
```
Author: @HuskyHacks

TENNNNNN-HUT!

Welcome to the Go Dojo, gophers in training!

Go malware is on the rise. So we need you to sharpen up those Go reverse engineering skills. We've written three simple CrackMe programs in Go to turn you into Go-binary reverse engineering ninjas!

First up is the easiest of the three. Go get em!
```

### Steps

I found two different ways to solve this challenge.  Both challenges first started with downloading the GoCrackMe1.zip.  I extracted the file and ran it against the file utility.  I discovered its a elf binary written in Golang.

```bash
GoCrackMe1: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), statically linked, Go BuildID=XTzA9g-rxSFKyebZYVXI/BFzZeSPLsNjAFEvjiSub/nTgut0H_UB7B79xaGq7-/X7kvo6zmAQOjIJV9zPwd, with debug_info, not stripped
```

Running the program we get an access denied message.

![](/static/2024-HuntressCTF/gcm1-0.png)

I opened IDA-Free on on my linux host and started to look at the assembly in a graph view and would also use the list view. With IDA-Free, you can hit the space bar to bounce between. 

** Also please note, I barely know what i'm doing, hopefully the writeup is accurate terminology! **

### Solution 1 - Patching the program

Quickly I saw at instruction `00000000004836AF` that it moves the decrypted into the rbx register with references to flag.  

![](/static/2024-HuntressCTF/gcm1-1.png)

Moving to Graph view, I see at the bottom of the function is there is a jz function to move to move the program to instruction `0x0000000000483719` where we are presented with the `Access Denied!` message. 

Before moving on, `jz` means Jump if Zero. If the zero flag is set before reaching this instruction.  Next, there is also `jnz` which is Jump if Not Zero. Here, we can set a specific location to jump to if the flag is set to 0. 

Now, looking at the graph view again. We see this visualized that the program right now will jump to the function to deny access.

![](/static/2024-HuntressCTF/gcm1-2.png)

I changed the instruction from `jz` to `jnz`.  Since the program is sending a 0 flag.  I left clicked on `jz      short loc_483719` and select Edit -> Patch Program -> Assemble. 

In the popup window change the instruction to jnz. 

![](/static/2024-HuntressCTF/gcm1-3.png)

After updating this value, I went to Edit -> Patch Program -> Apply Patches to Input File ...

Back to terminal I ran the program and received the flag!

![](/static/2024-HuntressCTF/gcm1-4.png)

### Solution 2 - Decompile and Evaluate Code 

For the second solution, I located the main_main function and pressed F5 for IDA-Free to attempt to decompile the code.  Looking at the code, I noticed what looked like an encoded/encrypted string. 

![](/static/2024-HuntressCTF/gcm1-5.png)

Admittedly, I used ChatGPT to evaluate the code and perform the XOR operation to get the flag.  From what I understand, the application the string `v17` is the encoded string. runtime_makeslice creates a byte slice of 38 characters in length.  Next, the XOR operations happens with `0x56`.  Knowing this, I used Cyberchef to perform the XOR operation and get the flag.

![](/static/2024-HuntressCTF/gcm1-6.png)


Flag: flag{bb59566e21f55e5680d589f3dbbec0f8}

