---
title: 2024 HuntressCTF - X-RAY 
date: 2024-10-12T07:00:00-07:00
tags:
  - 
image: /2024-HuntressCTF/xray.png
---

### Summary
```
Author: @JohnHammond

The SOC detected malware on a host, but antivirus already quarantined it... can you still make sense of what it does?
```

### Steps

This was a tricky challenge. I ended up having to combe through John Hammond's youtube challenge where I thankfully stumbled upon this video [Recover Quarantined Malware]("https://www.youtube.com/watch?v=K60kriw4o44").  Here John shows a new tool called [Dexray](https://hexacorn.com/d/DeXRAY.pl).  This tool can extract the original malware from a quarantined defender file.  

Before extracting the malware, I looked at the file `x-ray` and here was no header signature and the header was not documented on the internet that I could find. 

Next, I used the tool and extracted the malware from the quarantined file.

![](/static/2024-HuntressCTF/x1.png)

This created an `x-ray.00000184_Defender.out` file which was a PE file. I renamed the file to `xray.exe` and moved it to my Windows VM. I started by looking at the file properties and I see that Product Name is `stagetwo` and the Original filename was `stagetwo.dll`.  So I was wrong in assuming this was an .exe.  

![](/static/2024-HuntressCTF/x2.png)

I loaded stagetwo.dll into dnspy and started to look at the code. After a little time doing the code review, I discovered  this chunk of code:

```c
Public Shared Sub Main(args As String())
			New StageTwo().main("", New StreamReader(Console.OpenStandardInput()))
			Dim array As Byte() = StageTwo.load("15b279d8c0fdbd7d4a8eea255876a0fd189f4fafd4f4124dafae47cb20a447308e3f77995d3c")
			Dim array2 As Byte() = StageTwo.load("73de18bfbb99db4f7cbed3156d40959e7aac7d96b29071759c9b70fb18947000be5d41ab6c41")
			Dim array3 As Byte() = StageTwo.otp(array, array2)
			Encoding.UTF8.GetString(array3)
		End Sub
```
I also noticed that StageTwo called the otp function, which looked like an xor operation.
```c
		Private Shared Function otp(data As Byte(), key As Byte()) As Byte()
			Dim array As Byte() = New Byte(data.Length - 1) {}
			For i As Integer = 0 To data.Length - 1
				array(i) = data(i) Xor key(i Mod key.Length)
			Next
			Return array
		End Function
```
I used CyberChef to XOR the strings and discoverd the flag.

![](/static/2024-HuntressCTF/x3.png)

Flag: flag{df26090565cb329fdc8357080700b621}