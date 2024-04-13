### SeImpersonatePrivilege
How to exploit SeImpersonatePrivilege with different ways 

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
