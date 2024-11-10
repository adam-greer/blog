---
title: 2024 HuntressCTF - System Code
date: 2024-10-08T07:00:00-07:00
tags:
  - 
image: /2024-HuntressCTF/systemcode.png
---

### Summary
```
Author: Truman Kain

Follow the white rabbit.

NOTE: Bruteforce is permitted for this challenge instance if you feel it is necessary.
```

### Steps

When starting this challenge we are presented with a red or blue pill.  The blue pill to redirect to a matrix screen with a text box.  If you input the incorrect  value, you'll receive this error: "Incorrect. You will receive the flag with the correct input.".  
At the bottom of the website is a credit link that will take you to the [matrix]("https://github.com/Rezmason/matrix") repo.  After several hours or not making any progress, I worked with ChatGPT to come up with a script to download the files from the repo and then perform a HTTP request to the same file on the challenge server and look for differences. 

```python
import os
import subprocess
import requests
from filecmp import cmp
RED_BOLD = "\033[1;31m"
RESET = "\033[0m"

# Step 1: Clone the repo if it hasn't been cloned yet
repo_url = "https://github.com/Rezmason/matrix"
repo_dir = "matrix_repo"

if not os.path.isdir(repo_dir):
    subprocess.run(["git", "clone", repo_url, repo_dir])

# Step 2: Define the base URL for the CTF server
ctf_base_url = "http://challenge.ctf.games:31711/"

# Step 3: Function to download a file from the CTF server
def download_ctf_file(ctf_url, ctf_file_path):
    response = requests.get(ctf_url)
    if response.status_code == 200:
        with open(ctf_file_path, "wb") as f:
            f.write(response.content)
        return True
    else:
        print(f"Failed to download {ctf_url}")
        return False

# Step 4: Walk through the repository files and compare each one
for root, dirs, files in os.walk(repo_dir):
    for file in files:
        # Construct the relative file path in the repo
        repo_file_path = os.path.join(root, file)
        relative_path = os.path.relpath(repo_file_path, repo_dir)
        
        # Construct the URL for the corresponding file on the CTF server
        ctf_url = ctf_base_url + relative_path
        ctf_file_path = "ctf_" + file

        # Download the file from the CTF server
        if download_ctf_file(ctf_url, ctf_file_path):
            # Compare the repo file with the CTF filei
            if cmp(repo_file_path, ctf_file_path, shallow=False):
                print(f"{relative_path}: Files are identical.")
            else:
                print(f"{RED_BOLD}{relative_path}: Files are different.{RESET}")
            
            # Remove the downloaded CTF file after comparison
            os.remove(ctf_file_path)
        else:
            print(f"{relative_path}: File not found on CTF server.")
```

The script will enumerate through the various files and you'll see if found that `config.js` was different. 

![](/static/2024-HuntressCTF/sc1.png)

After comparing the config.js file, I found `backupGlyphsTwr: ["a", "b", "c", "d", "e", "f"], // The characters to fallback to if glyphs fail to load`.

I spent time with BurpSuite to make sure the various .png files failed to load, but this never actually rendered a flag or helped make progress.  Eventually, I had ChatGPT create every permutation of `a+b+c+d+e+f` which resulted in a 720 line file.  I passed this to BurpSuite and used intruder to test each iteration, which turned out to be the flag.  
```
GET /enter=bfdaec HTTP/1.1
Host: challenge.ctf.games:31711
Accept-Language: en-US,en;q=0.9
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.6613.120 Safari/537.36
Accept: */*
Referer: http://challenge.ctf.games:31711//
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
![](/static/2024-HuntressCTF/sc2.png)



Flag: flag{dc9edf4624504202eec5d3fab10bbccd}