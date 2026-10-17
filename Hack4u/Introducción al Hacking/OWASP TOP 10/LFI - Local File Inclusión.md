___
- tags: #lfi #owasp 
___
Es una de las vulnerabilidades de seguridad informática que se produce cuando una aplicación web no valida adecuadamente las entradas de usuario, permitiendo a un atacante acceder a los **archivos locales** en el servidor web.
En muchos casos, los atacantes aprovechan la vulnerabilidad de LFI al abusar de parámetros de entrada en la aplicación web.
## Path Traversal
El atacante de Path Traversal, el atacante utiliza caracteres especiales y caracteres de escape en los parámetros de entrada para navegar a través de los directorios del servidor web y acceder a archivos en ubicaciones sensibles del sistema.

## Prevención
Para prevenir los ataques LFI, es importante que los desarrolladores validen y filtren adecuadamente la entrada del usuario, limitando el acceso a los recursos del sistema y asegurándose de que los archivos sólo se puedan incluir desde ubicaciones permitidas.

## Wrappers
### Filter
```txt
://filter/convert.base64-encode/resource=
```

### rot13
```txt
php://filter/read=string.rot13/resource=<archivo>
```

### zip
```txt
zip://<archivo zip>%23<archivo php>
```

___
## Referencia
- [Wrappers php](https://deephacking.tech/php-wrappers-pentesting-web/).