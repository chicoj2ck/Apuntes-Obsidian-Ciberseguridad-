___
- tags: #abusing_privilege #user_groups 
___
## Contexto
En el contexto de Linux, los **grupos** se utilizan para **organizar** a los usuarios y **asignar** **permisos** para acceder a los recursos del sistema. Los usuarios pueden pertenecer a uno o varios grupos, y los grupos pueden tener diferentes niveles de permisos para acceder a los recursos del sistema.

Existen grupos especiales en Linux, como **'lxd'** o **'docker'**, que se utilizan para permitir a los usuarios ejecutar contenedores de manera segura y eficiente. Sin embargo, si un usuario malintencionado tiene acceso a uno de estos grupos, podría aprovecharlo para obtener privilegios en el sistema.

## Añadiendo al grupo
```shell
usermod -a -G docker chicoj2ck
```
## Eliminando del grupo
```shell
gpasswd -d chicoj2ck docker
```
