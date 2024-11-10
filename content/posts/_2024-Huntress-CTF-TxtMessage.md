---
title: 2024 HuntressCTF - TXT Message
date: 2024-10-01T07:00:00-07:00
tags:
  - 
image: /2024-HuntressCTF/txtmessage.png
---

### Summary
```
Author: @JohnHammond

Hmmm, have you seen some of the strange DNS records for the ctf.games domain? One of them sure is odd...
```

### Steps

In the challenge description, the `od` was a hyperlink to https://en.wikipedia.org/wiki/Od_(Unix).  My first assumption was that i'm going to have to use the OD utility to decode the text.  I performed an nslookup against the TXT type and received this response:
```bash
nslookup -type=txt ctf.games                                                                                                                 
Server:		192.168.240.2
Address:	192.168.240.2#53

Non-authoritative answer:
ctf.games	text = "146 154 141 147 173 061 064 145 060 067 062 146 067 060 065 144 064 065 070 070 062 064 060 061 144 061 064 061 143 065 066 062 146 144 143 060 142 175"

Authoritative answers can be found from:
```

I spent some time with the od utility, but was unsuccessful in getting the ASCII conversion.  Then I tested with CyberChef's `From Octal` and got the flag.

For fun, here is an automated approach:
```bash
nslookup -type=txt ctf.games | grep text | cut -d "=" -f 2 | tr -d '"' |  awk '{for(i=1;i<=NF;i++) printf("%c", strtonum("0" $i)); print ""}'
```

Flag: flag{14e072f705d45882401d141c562fdc0b}