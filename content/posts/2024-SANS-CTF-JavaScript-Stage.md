---
title: 2024 SANS Offensive Operation CTF - JavaScript Stage 001-003
date: 2024-02-28T07:00:00-07:00
tags:
  - javascript
image: 
---


### Summary
```
We heard you like JavaScript? So we scrambled some nice JavaScript ☕ code for you to review! Review the provided code snippet and send appropriate API request to get the flag!
```

### JavaScript 001

![](/2024sansctf/js001.png)

Using the provided javascript I used the browsers console to help piece together the string.  

![](/2024sansctf/js001-2.png)

As we see in the screenshot, the value for `"b" + "a" + +"a" + "a"` is equals to `baNaNa`.  This happens because the javascript is processing the space and reporting it as NaN (Not-a-Number). 

Using this value, I sent a post request to the endpoint to get the flag
```bash
curl -X POST http://js.pwn.site:1995/api/stages/1 -H "Content-Type: application/json" -d '{"password":"baNaNa"}'
```
I received the following response:
`{"flag":"flag{B-baNaNa?baNaNa!baNaNa!baNaNa!}"}% `

### JavaScript 002

![](/2024sansctf/js002.png)

In challenge 002 we need to determine the answer for `0.1 + 0.2` as a password to the /2 endpoint.  Using the same technique, I let the browser perform the operation for me giving me a value of `0.30000000000000004`

![](/2024sansctf/js002-2.png)

Next, I again sent a POST request to the `/2` endpoint. 

```bash
curl -X POST http://js.pwn.site:1995/api/stages/2 -H "Content-Type: application/json" -d '{"password":"0.30000000000000004"}'
```

The system provided the following flag.
`{"flag":"flag{IEEE-754-floating-with-you!}"}% `

### JavaScript 003

![](/2024sansctf/js003.png)

For JavaScript challenge 003, this technique utilized jsfuck to obfuscate the javascript.  However, the browser will easily decode this into the intended string for us as `octocat`.

![](/2024sansctf/js003-2.png)

Again, I sent another POST request and got the flag.

```bash
curl -X POST http://js.pwn.site:1995/api/stages/3 -H "Content-Type: application/json" -d '{"password":"octocat"}'
```

`{"flag":"flag{w31rD-j4v45cr1p7-m0m3nt!}"}% `




