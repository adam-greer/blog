---
title: 2024 HuntressCTF - Red Phish Blue Phish
date: 2024-10-02T07:00:00-07:00
tags:
  - 
image: /2024-HuntressCTF/redphishbluephish.png
---

### Summary
```
Author: Truman Kain (@truman.huntress), Adam Rice (@adam.huntress)

You are to conduct a phishing excercise against our client, Pyrch Data.

We've identified the Marketing Director, Sarah Williams (swilliams@pyrchdata.com), as a user susceptible to phishing.

Are you able to successfully phish her? Remember your OSINT ;)

NOTE: The port that becomes accessible upon challenge deployment is an SMTP server. Please use this for sending any phishing emails.

You will not receive an email/human response as the mail infrastructure for this challenge is emulated.
```

### Steps

I started the container for the challenge and was given a hostname to connect to.  Upon connecting to the system, I quickly discovered that it was an SMTP server.  I also googled the hostname for the Sarah Williams, and discovered the team members for the company [Team]("https://pyrchdata.com/team").  I ran into issues with terminating the email, and found that I needed to use the `-C | Send CRLF as line-ending` flag. 
Using the same email format as SWilliams, I sent an email from each team memeber and as I enumerated through the staff, I found that I discovered the flag when the sender was Joe Daveren.  

```bash
MAIL FROM:<jdaveren@pyrchdata.com>
250 OK
RCPT TO:<swilliams@pyrchdata.com>
250 OK
DATA
354 End data with <CR><LF>.<CR><LF>
Subject: Immediate

.
250 OK. flag{54c6ec05ca19565754351b7fcf9c03b2}
 sent 938, rcvd 1370
```

Flag: flag{54c6ec05ca19565754351b7fcf9c03b2}