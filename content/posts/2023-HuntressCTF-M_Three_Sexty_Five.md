---
title: 2023 HuntressCTF - M Three Sixty Five
date: 2023-11-01T07:00:00-07:00
tags:
  - m365
  - powershell
  - AADInternals
image: /2023-HuntressCTF/m365.png
---

### Summary - General Info
```
Author: @David Carter

Welcome to our hackable M365 tenant! Can you find any juicy details, like perhaps the street address this organization is associated with?
```

### Steps

Upon authenicating to the server, I noticed the ADDInternal suite of tools was being used.  I looked at the documenation for [AADInternals by DrAzureAD](https://aadinternals.com/aadinternals/#Get-AADIntCompanyInformation) and found a cmdlet for ```Get-AADIntCompanyInformation``` which had the flag.
Flag:  ```flag{dd7bf230fde8d4836917806aff6a6b27}```

![](/2023-HuntressCTF/m365geninfo.png)


### Summary - Conditional Access

```
Author: @David Carter

This tenant looks to have some odd Conditional Access Policies. Can you find a weird one?


```

### Steps

Referencing the documenation again there was a cmdlet for ```Get-AADIntConditionalAccessPolicies``` which listed our the conditional access polilcy and the flag was in the displayName field.
Flag ```flag{d02fd5f79caa273ea535a526562fd5f7}```

![](/2023-HuntressCTF/m365ca.png)

### Summary - Teams

```
Author: @David Carter

We observed saw some sensitive information being shared over a Microsoft Teams message! Can you track it down?

```

### Steps

Using the ```Get-AADIntTeamsMessage``` cmdlet I found there was a flag that was sent with teams.

Flag: ```flag{f17cf5c1e2e94ddb62b98af0fbbd46e1}```

![](/2023-HuntressCTF/teamsflag.png)


### Summary - The President
```
Author: @David Carter

One of the users in this environment seems to have unintentionally left some information in their account details. Can you track down The President?
```

Next, I used ```Get-AADIntUsers  | select UserPrincipalName, DisplayName, Department, Title``` to get a quick view into the users, department and title of the User objects in this domain.
```powershell
UserPrincipalName                       DisplayName       Department           Title
-----------------                       -----------       ----------           -----
LeeG@4rhdc6.onmicrosoft.com             Lee Gu            Manufacturing        Director
AlexW@4rhdc6.onmicrosoft.com            Alex Wilber       Marketing            Marketing Assistant
HuntressCTFAdmin@4rhdc6.onmicrosoft.com FNU LNU                                
HackMe@4rhdc6.onmicrosoft.com           CompromisedAcct                        
JohannaL@4rhdc6.onmicrosoft.com         Johanna Lorenz    Engineering          Senior Engineer
LynneR@4rhdc6.onmicrosoft.com           Lynne Robbins     Retail               Planner
HenriettaM@4rhdc6.onmicrosoft.com       Henrietta Mueller R&D                  Developer
JoniS@4rhdc6.onmicrosoft.com            Joni Sherman      Legal                Paralegal
AdeleV@4rhdc6.onmicrosoft.com           Adele Vance       Retail               Retail Manager
DiegoS@4rhdc6.onmicrosoft.com           Diego Siciliani   HR                   HR Manager
LidiaH@4rhdc6.onmicrosoft.com           Lidia Holloway    Engineering          Product Manager
NestorW@4rhdc6.onmicrosoft.com          Nestor Wilke      Operations           Director
PattiF@4rhdc6.onmicrosoft.com           Patti Fernandez   Executive Management President
PradeepG@4rhdc6.onmicrosoft.com         Pradeep Gupta     Finance              Accountant
GradyA@4rhdc6.onmicrosoft.com           Grady Archie      R&D                  Designer
MeganB@4rhdc6.onmicrosoft.com           Megan Bowen       Marketing            Marketing Manager
IsaiahL@4rhdc6.onmicrosoft.com          Isaiah Langer     Sales                Sales Rep
MiriamG@4rhdc6.onmicrosoft.com          Miriam Graham     Sales & Marketing    Director
```

Knowing that the President is Patti Fernandez, I want to next few all details on this account. I used ```powersehell get-AADIntUser -UserPrincipalName "PattiF@4rhdc6.onmicrosoft.com"``` and found the flag listed in the PhoneNumber field.
Flag: ```flag{1e674f0dd1434f2bb3fe5d645b0f9cc3}```

![](/2023-HuntressCTF/m365phonenumber.png)

### Steps





