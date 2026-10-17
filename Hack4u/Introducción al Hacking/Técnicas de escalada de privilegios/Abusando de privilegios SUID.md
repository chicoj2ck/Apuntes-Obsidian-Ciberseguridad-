___
- tags: #abusing_privilege #suid
___
Un privilegio **SUID(Set User ID)** es un permiso que se pude establecer en un archivo binario en sistemas Unix/Linux. Este permiso le da al usuario que ejecuta el archivo los **mismos privilegios** que el **propietario** del archivo.
El abuso de privilegios SUID es una técnica utilizada por los atacantes para elevar su nivel de acceso en un sistema comprometido. Si un atacante es capaz de obtener acceso a un archivo binario con permisos SUID, puede ejecutar comandos con privilegios especiales y realizar acciones maliciosas en el sistema.

## Listando Binarios SUID
```shell
find / -perm -4000 2>/dev/null
```