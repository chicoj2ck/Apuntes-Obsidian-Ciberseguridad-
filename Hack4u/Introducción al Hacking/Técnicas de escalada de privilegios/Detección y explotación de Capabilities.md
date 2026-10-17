___
- tags: #abusing_privilege #capabilities
___
En sistemas Linux, las **capabilities** son una funcionalidad de seguridad que permite a los usuarios realizar acciones que normalmente requieren privilegios de superusuario (**root**), sin tener que concederles acceso completo de superusuario. Esto se hace para mejorar la seguridad, ya que un proceso que solo necesita ciertos privilegios puede obtenerlos sin tener que ejecutarse como root.

## Tipos
### Permisos efectivos (effective capabilities)
Son los permisos que se aplican directamente al proceso que los posee. Estos permisos determinan las acciones que el proceso puede realizar. Por ejemplo, la capability “**CAP_NET_ADMIN**” permite al proceso modificar la configuración de red.
### Permisos heredados (inheritable capabilities)
Son los permisos que se heredan por los procesos hijos que son creados. Estos permisos pueden ser adicionales a los permisos efectivos que ya posee el proceso padre. Por ejemplo, si un proceso padre tiene la capability “**CAP_NET_ADMIN**” y esta capability se configura como heredable, entonces los procesos hijos también tendrán la capability “**CAP_NET_ADMIN**“.
### Permisos permitidos (permitted capabilities)
Son los permisos que un proceso tiene permitidos. Esto incluye tanto permisos efectivos como heredados. Un proceso solo puede ejecutar acciones para las que tiene permisos permitidos. Por ejemplo, si un proceso tiene la capability “**CAP_NET_ADMIN**” y la capability “**CAP_SETUID**” configurada como permitida, entonces el proceso puede modificar la configuración de red y cambiar su **UID** (**User ID**).

## Buscando Capabilities
```shell
# busca archivos con capabilities de forma recursiva
# desde la raiz
getcap -r / 2>/dev/null
```