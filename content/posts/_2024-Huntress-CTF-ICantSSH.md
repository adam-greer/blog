---
title: 2024 HuntressCTF - I Can't SSH
date: 2024-10-09T07:00:00-07:00
tags:
  - 
image: /2024-HuntressCTF/ssh.png
---

### Summary
```
Author: @JohnHammond

I've got this private key... but why can't I SSH?

Download the file(s) below and press Start on the top-right to begin this challenge.
Connect with:
# Password is "userpass"
ssh -p 30442 user@challenge.ctf.games
```

### Steps

Along with the docker instance there is an attached private id_ssh key. When I first attempted to ssh into the instance with the private key, I get a unprotected file warning. To fix the ssh key:

```bash
ssh -p 30442 user@challenge.ctf.games -i id_rsa 
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0664 for 'id_rsa' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "id_rsa": bad permissions
```

I've ran into this issue many times in the past. All I needed to do was update the permissions on the key using the following:
```
chmod 600 ./id_rsa
```
Then we can SSH without any issues:

```bash
sh user@challenge.ctf.games -p 30442 -i id_rsa
user@i-cant-ssh-fa043244a39c509c-f7d49469-jl4bg:~$
```
 Lastly, flag.txt is in the home directory. 

Flag: flag{ee1f28722ec1ce1542aa1b486dbb1361}