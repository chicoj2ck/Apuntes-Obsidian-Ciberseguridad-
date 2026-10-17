___
- tags: #sudoers #abusing_privilege
___
## Sudoers
El archivo **/etc/sudoers** es un archivo de configuración en sistema Linux que se utiliza para controlar el acceso de los usuarios a las diferentes acciones que pueden realizar en el sistema.
Este archivo contiene una lista de usuarios que tienen permisos para realizar tareas de administración en el sistema.
## Sudo
El comando **"sudo"** permite a los  usuarios ejecutar comandos como un super usuario o como otro usuario con privilegios especiales. El archivo sudoers especifica qué usuarios pueden ejecutar qué comandos con sudo y con privilegios.

## Elevando privilegios
Abusar de los privilegios a nivel de **sudoers** es una técnica utilizada por los atacantes para elevar su nivel de acceso en un sistema comprometido. Si un atacante es capaz de obtener acceso a una cuenta con permisos de sudo en el archivo sudoers, puede ejecutar comandos con privilegios especiales y realizar acciones maliciosas en el sistema.

## Comandos útiles
### Listar los permisos de sudo de un usuario
```shell
sudo -l
```
## Prevención
Para prevenir el abuso de privilegios a nivel de sudoers, se recomienda mantener los permisos adecuados en el archivo sudoers y limitar el número de usuarios con permisos de sudo. Además, es importante monitorear regularmente el archivo sudoers y buscar cambios inesperados o sospechosos en su contenido.
___
## Referencia
- [GTFOBins](https://gtfobins.github.io/).