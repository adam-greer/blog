---
title: 2024 HuntressCTF - Base-p-
date: 2024-10-08T07:00:00-07:00
tags:
  - 
image: /2024-HuntressCTF/basep.png
---

### Summary
```
Author: Izzy Spering

That looks like a weird encoding, I wonder what it's based on.
```

### Steps

Looking at the text file for the challenge I see this:
```
楈繳籁萰杁癣怯蘲詶歴蝕絪敪ꕘ橃鹲𠁢腂𔕃饋𓁯𒁊鹓湵蝱硦楬驪腉繓鵃舱𒅡繃絎罅陰罌繖𔕱蝔浃虄眵虂𒄰𓉋詘襰ꅥ破ꌴ顂𔑫硳蕈訶𒀹饡鵄腦蔷樸𠁺襐浸椱欱蹌ꍣ鱙癅腏葧𔕇鱋鱸𓁮聊聍ꄸꈴ陉𔕁框ꅔ𔕩𔕃驂虪祑𓅁聨朸聣摸眲葮𖠳鵺穭𒁭豍摮饱恕𓉮詔葉鰸葭楷洳面𔕃𔑒踳𔐸杅𐙥湳橹驳陪楴氹橬𓄱蝔晏稸ꄸ防癓ꉁ𖡩鵱聲ꍆ稸鬶魚𓉯艭𔕬輷茳筋𔑭湰𓄲怸艈恧襺陷项譶ꍑ衮汮蹆杗筌蹙怰晘缸睰脹蹃鹬ꕓ脶湏赑魶繡罢𒉁荶腳ꌳ蕔𔐶橊欹𖥇繋赡𐙂饎罒鵡𒉮腙ꍮ楑恤魌虢昹𒅶效楙衎𔕙ꉨ𓈸𔑭樯筶筚絮𓁗浈豱ꉕ魔魧蕕聘筣鹖樫ꍖ汸湖萰腪轪𓉱艱絍笹艨魚詇腁𒁮陴顮虂癁
```

The challenge's name is Base-p-.  The `-p-` reminds me of the all ports commands on nmap which reminded of a challenge last year where I had to use Base65536.  Trying that same approach I was able to decode the text another chunk of base64 text.

```
H4sIAG0OA2cA/+2QvUt6URjHj0XmC5ribzBLCwKdorJoSiu9qRfCl4jeILSICh1MapCINHEJpaLJVIqwTRC8DQ5BBQ0pKtXUpTej4C4lBckvsCHP6U9oadDhfL7P85zzPTx81416LYclYgEAOLgOGwKgxgnrJKMK8j4kIaAwF3TjiwCwBejQQDAshK82cKx/2BnO3xzhmEmoMWn/qdU+ntTUIO8gmOw438bbCwRv3Y8vE2ens9y5sejat497l51sTRO18E8j2aSAAkixqhrKFl8E6fZfotmMlw7Z3NKFmvp92s8+HMg+zTwaycvVQlnSn7FYW2LFYY0+X18JpB9LCYliSm6LO9QXvfaIbJAqvNsL3lTP6vJ596GyKIaXBnNdRJahnqYLnlQ4d+LfbQ91vpH0Y4NSYwhk8tmv/5vFZFnHWrH8qWUkTfgfUPXKcFVi+5Vlx7V90OjLjZqtqMMH9FhMZfGUALnotancBQAA
```

I plugged in this into CyberChef and used Magic and it determine it was base64 decoded with gunzip, and this recipe became a valid PNG file.

![](/static/2024-HuntressCTF/b1.png)

With CyberChef I can render the image and I see its an image with 13 color bars.

![](/static/2024-HuntressCTF/b2.png)

I uploaded the image to [ImageColorPicker]("https://imagecolorpicker.com/").

Here I selected each color and copied the RGB value cyberchef.

![](/static/2024-HuntressCTF/b3.png)

After some modifying the values, it was found to be ASCII. Staying with CyberChef I stripped away the alpha portion of the RGB (255's) and then convert it from Decimal, resulting in the flag.

![](/static/2024-HuntressCTF/b4.png)

Flag: flag{586cf8c849c9730ea7b2112fff39ff6a}