---
title: 2024 HuntressCTF - Obfuscation Station
date: 2024-10-13T07:00:00-07:00
tags:
  - 
image: /2024-HuntressCTF/obfuscationstation.png
---

### Summary
```
Author: @resume

You've reached the Obfuscation Station!
Can you decode this PowerShell to find the flag?
```

### Steps

Within the .zip file was a file called chal.ps1 and it was an obfuscated script. 
```powershell
(nEW-objECt  SYstem.iO.COMPreSsIon.deFlaTEStREAm( [IO.mEmORYstreAM][coNVERt]::FROMBAse64sTRING( 'UzF19/UJV7BVUErLSUyvNk5NMTM3TU0zMDYxNjSxNDcyNjexTDY2SUu0NDRITDWpVQIA') ,[io.COmPREssioN.coMpreSSioNmODE]::DeCoMpReSS)| %{ nEW-objECt  sYStEm.Io.StREAMrEADeR($_,[TeXT.encodiNG]::AsCii)} |%{ $_.READTOENd()})| & ( $eNV:cOmSPEc[4,15,25]-JOin'')
```

Within my Windows environment, I cleared the Windows PowerShell Event logs and executed the script. I have powershell logging enabled like to let Windows handle the deobfuscation if possible.  As expected, I found the flag within the event logs. 

![](/static/2024-HuntressCTF/os1.png)






Flag: flag{3ed675ef0343149723749c34fa910ae4}