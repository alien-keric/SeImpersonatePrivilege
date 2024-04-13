### SeImpersonatePrivilege
How to exploit SeImpersonatePrivilege with different ways, it is also gud to check what version of operating system were dealing with
``
C:\Users\Public\Desktop>systeminfo | findstr /B /C:"Host Name" /C:"OS Name" /C:"OS Version" /C:"System Type" /C:"Hotfix(s)"
systeminfo | findstr /B /C:"Host Name" /C:"OS Name" /C:"OS Version" /C:"System Type" /C:"Hotfix(s)"
Host Name:                 REMOTE
OS Name:                   Microsoft Windows Server 2019 Standard
OS Version:                10.0.17763 N/A Build 17763
System Type:               x64-based PC
Hotfix(s):                 4 Hotfix(s) Installed.
```

## Assume you have exploi a windows operating system and you run the **whoami/priv** you find that you can exploit to **nt authority\system**  throught tokenImpersonate, there many ways do this but when doing pentesting, in this blog am going to upload every technique i use when i meet this enviroment when approaching a target.

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

