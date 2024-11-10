---
title: 2024 HuntressCTF - Malibu
date: 2024-10-04T07:00:00-07:00
tags:
  - 
image: /2024-HuntressCTF/malibu.png
---

### Summary
```
Author: Truman Kain

What do you bring to the beach?

NOTE: There are two things to note for this challenge.
This service takes a bit more time to start. If you see a Connection refused, please wait a bit more.
This service will not immediately respond or prompt you... it is waiting for your input. If you just hit Enter, you will see what it is.
Extra tip, once you know what the service is, try connecting in a better way. Then use some of the context clues and critical thinking based off its response and the challenge description. You don't need any bruteforcing once you understand the infrastructure and enumerate. ;)
```

### Steps

I started by connecting to the service but I used `nc -vv challenge.ctf.games 30738` but didn't see any real indicators at this time.
![](/static/2024-HuntressCTF/m1.png)

I sent a HTTP request to the service using the following:
```
GET / HTTP/1.1
Host: challenge.ctf.games

HTTP/1.1 403 Forbidden
Accept-Ranges: bytes
Content-Length: 254
Content-Type: application/xml
Server: MinIO
Strict-Transport-Security: max-age=31536000; includeSubDomains
Vary: Origin
Vary: Accept-Encoding
X-Amz-Id-2: dd9025bab4ad464b049177c95eb6ebf374d3b3fd1af9251148b658df7ac2e3e8
X-Amz-Request-Id: 17FB5F2F48151F15
X-Content-Type-Options: nosniff
X-Ratelimit-Limit: 59
X-Ratelimit-Remaining: 59
X-Xss-Protection: 1; mode=block
Date: Fri, 04 Oct 2024 22:05:38 GMT

<?xml version="1.0" encoding="UTF-8"?>
<Error><Code>AccessDenied</Code><Message>Access Denied.</Message><Resource>/</Resource><RequestId>17FB5F2F48151F15</RequestId><HostId>dd9025bab4ad464b049177c95eb6ebf374d3b3fd1af9251148b658df7ac2e3e8</HostId></Error>
```

After some time, I realized from HTTP response headers that we are using the Minio Service and using an S3 bucket, which also aligns to the challenge name. I got tired of typing in the HTTP request into nc, so I switched to curl.  Next, I sent an HTTP request to /bucket and discovered it will output the various keys.
`curl http://challenge.ctf.games:30738/bucket`.  The .xml file was fairly long, so I 

I prompted ChatGPT to generate a python script to enumerate the .xml file and download each file from the associated key value. 
```python
import xml.etree.ElementTree as ET
import requests
import os

# Load the XML file
tree = ET.parse('bucket')
root = tree.getroot()

# Define base URL
base_url = "http://challenge.ctf.games:30738/bucket/"

# Create a directory to save the downloaded files if it doesn't exist
download_dir = 'downloads'
os.makedirs(download_dir, exist_ok=True)

# Find all 'Key' elements and construct URLs
urls = [base_url + key.text for key in root.findall('.//{http://s3.amazonaws.com/doc/2006-03-01/}Key')]

# Download each file
for url in urls:
    # Get the filename from the URL
    filename = os.path.join(download_dir, url.split('/')[-1])
    
    # Download the file
    print(f"Downloading {url}")
    response = requests.get(url)
    
    if response.status_code == 200:
        # Save the file
        with open(filename, 'wb') as file:
            file.write(response.content)
        print(f"File saved as {filename}")
    else:
        print(f"Failed to download {url}. Status code: {response.status_code}")

print("Download completed!")
```
![](/static/2024-HuntressCTF/m2.png)

I manually started to look through the files, but decided to first grep for the flag.
```bash
$ grep -rl "flag" ./
./YaxxoCf47cWL0BAQ
```
I found that the string flag was in the file "YaxxoCf47cWL0BAQ". 

![](/static/2024-HuntressCTF/m3.png)

Flag: flag{800e6603e86fe0a68875d3335e0daf81}