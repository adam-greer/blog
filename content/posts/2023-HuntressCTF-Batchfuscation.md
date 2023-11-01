---
title: 2023 HuntressCTF - Batchfuscation
date: 2023-11-01T07:00:00-07:00
tags:
  - malware
  - batch
  - deobfuscation
image: /2023-HuntressCTF/batch.png
---

### Summary
```
Author: @JohnHammond

I was reading a report on past Trickbot malware, and I found this sample that looks a lot like their code! Can you make any sense of it?
```

### Steps


The the start of this code was heavly obfuscated and after getting an understanding of what was happening I started to manually deobfuscate the code.  Looking at the code it looks like multiple variables tired together.
```bash
@echo off
set bdevq=set
%bdevq% grfxdh= 
%bdevq%%grfxdh%mbbzmk==
%bdevq%%grfxdh%xeegh%mbbzmk%/
%bdevq%%grfxdh%jeuudks%mbbzmk%a
%bdevq%%grfxdh%rbiky%mbbzmk%c
%bdevq%%grfxdh%wzirk%mbbzmk%m
%bdevq%%grfxdh%naikpbo%mbbzmk%d
%bdevq%%grfxdh%ltevposie%mbbzmk%e
%bdevq%%grfxdh%uqcqswo%mbbzmk%x
%bdevq%%grfxdh%zvipzis%mbbzmk%i
%bdevq%%grfxdh%kquqjy%mbbzmk%t
%bdevq%%grfxdh%kmgnxdhqb%mbbzmk% 
%bdevq%%grfxdh%%xeegh%%jeuudks%%grfxdh%bpquuu%mbbzmk%4941956 %% 4941859
%rbiky%%wzirk%%naikpbo%%kmgnxdhqb%%xeegh%%rbiky%%kmgnxdhqb%%ltevposie%%uqcqswo%%zvipzis%%kquqjy%%kmgnxdhqb%%bpquuu%
%bdevq%%grfxdh%grtoy%mbbzmk%%=exitcodeAscii%
%bdevq%%grfxdh%%xeegh%%jeuudks%%grfxdh%fqumc%mbbzmk%9273642 %% 9273544
%rbiky%%wzirk%%naikpbo%%kmgnxdhqb%%xeegh%%rbiky%%kmgnxdhqb%%ltevposie%%uqcqswo%%zvipzis%%kquqjy%%kmgnxdhqb%%fqumc%
%bdevq%%grfxdh%kbhoesxh%mbbzmk%%=exitcodeAscii%
%bdevq%%grfxdh%%xeegh%%jeuudks%%grfxdh%uhtsvvtj%mbbzmk%9196704 %% 9196605
%rbiky%%wzirk%%naikpbo%%kmgnxdhqb%%xeegh%%rbiky%%kmgnxdhqb%%ltevposie%%uqcqswo%%zvipzis%%kquqjy%%kmgnxdhqb%%uhtsvvtj%
%bdevq%%grfxdh%fxflckau%mbbzmk%%=exitcodeAscii%
%bdevq%%grfxdh%%xeegh%%jeuudks%%grfxdh%anbayva%mbbzmk%2699100 %% 2699000
%rbiky%%wzirk%%naikpbo%%kmgnxdhqb%%xeegh%%rbiky%%kmgnxdhqb%%ltevposie%%uqcqswo%%zvipzis%%kquqjy%%kmgnxdhqb%%anbayva%
%bdevq%%grfxdh%pxesvvz%mbbzmk%%=exitcodeAscii%
```

I started to manually replace the varables with the ASCII repersesntation.  For exmaple `%bdevq%` was equal to to a space.  So I did a find and replace accross all the code and updated it.  As I continued to work through this, I was able to get to code that looked like this:
```bash
set/abpquuu=4941956 %% 4941859
cmd/cexit(4941956 %% 4941859)
```

I'm sure there was a much faster and more automated approach for this, but next, edited the script to include `@echo on` and added the following line of code for each set variable: 
```bash
echo  the exit code for bpquuu:%bpquuu% is %=exitcodeAscii%
```

then I executed `.\batchuscation.bat > log.txt` and reviewed the logs.  Using powershell we can search through the log file:
```powershell
$log = Get-Content .\log.txt
$log | Select-String "^ the exit"
```
 
and I see the similar results:
```powershell
 the exit code for bpquuu:97 is a
 the exit code for kbhoesxh:98 is b
 the exit code for fxflckau:99 is c
 the exit code for anbayva:100 is d
 the exit code for sotjqqk:101 is e
 the exit code for kefdskui:102 is f
 the exit code for swjhnkfh:103 is g
 the exit code for jorbiysyv:104 is h
```

All the results turned out to be `a-z0-9{}?:.=,_`

I replaced all iterations of of the exit code with the repsected ASCII value and as I continued to manually deobfuscate the code, I started to assemble hints towards the flag, as seen in the code snippet below:

```bash
rem set bmvyrslfeccacqusqmfuwrwujksntppamchwahyvppzukumaairvsfewopezxzb=qylsgossatalvcqkwdctargrsonnpwggmlcnvtbzpdarq
:: set flag_character%wpwjwymw%%flopojsse%=3
rem set cazpqeswumqnwtrafieobxifznvlpdnqexmsbhucd=yptczbzgutmefluyvwofgzjtgjeyorkx
```

After updating all variables with the ASCII numbers, I used powershell to search for the flag:
```powershell
:: set flag_character34=d
:: set flag_character20=3
:: set flag_character2=l
:: set flag_character1=f
:: set flag_character8=a
:: set flag_character10=6
:: set flag_character35=1
:: set flag_character37=a
:: set flag_character18=b
:: set flag_character32=b
:: set flag_character14=d
:: set flag_character16=b
:: set flag_character9=d
:: set flag_character6=a
:: set flag_character24=6
:: set flag_character28=3
:: set flag_character19=f
:: set flag_character33=9
:: set flag_character13=3
:: set flag_character23=c
:: set flag_character30=0
:: set flag_character22=a
:: set flag_character25=6
:: set flag_character15=0
:: set flag_character38=}
:: set flag_character27=9
:: set flag_character4=g
:: set flag_character31=d
:: set flag_character21=1
:: set flag_character36=9
:: set flag_character12=e
:: set flag_character5={
:: set flag_character7=c
:: set flag_character17=5
:: set flag_character26=3
:: set flag_character11=7
:: set flag_character3=a
:: set flag_character29=6
```

After re-arranging the flag order I got: `flag{acad67e3d0b5bf31ac6639360db9d19a}`