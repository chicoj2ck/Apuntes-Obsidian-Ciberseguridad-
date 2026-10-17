____
#machine #easy #nmap 
___

## Nmap
```sh
nmap -p- --open -sS -Pn -n -vvv --min-rate 5000 10.129.133.144 -oG all_ports

# -p-: todos los puertos
# --open: filtra la salida para mostrar los puertos abiertos
# -sS: Escaneo silencioso (SYN Scan), no completa el establecimiento de conexion TCP
# -Pn: No realiza descubrimiento de hosts (se asume como activo).
# -n: Evita la resolucion dns (reduce la cantidad de consultas)
# --min-rate 5000: establece que no envie menos de 5000 paquetes por segundo
# -oG: output grep -> guarda la informacion en un archivo grepable

PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack ttl 63
80/tcp open  http    syn-ack ttl 63
```

- Puerto 22 - ssh
- Puerto 80 - http (pagina web)

## Entramos a la pagina web
Redirige al dominio 2million.htb, por lo que tenemos que agregarlo a nuestro dns
```sh
nvim /etc/hosts

# agregamos el dominio

# ip 2million.htb
```
