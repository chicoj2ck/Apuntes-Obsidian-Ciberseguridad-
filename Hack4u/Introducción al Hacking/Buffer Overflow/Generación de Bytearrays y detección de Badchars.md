___
- tags: #buffer_overflow #badchars #bytearrays
___
## Mona.py
### Seteamos el directorio de trabajo
```shell
# En Inmmunity Debugger -> nos permite ejecutar archivos '.py'
!mona config -set workingfolder C:\Users\chicoj2ck\Desktop\Analysis
```

### Generamos un arreglo de bytes en el directorio anterior
```shell
!mona bytearrray
```

### Generamos un arreglo de bytes en el directorio anterior excluyendo el nullbyte
```shell
!mona bytearray -cpb "\x00"
```

## Verificamos los caracteres que son badchar
Verificamos que caracteres en hexadecimal no aparece en el dump del **Immunity Debugger**
### Ejemplo de dump
Seguimos lo que nos arroja en el **ESP** 
![[Pasted image 20251018182111.png]]
### Más zoom
Vemos que aparece el 01,02,03 ... pero luego del 09 se salta al 29 -> por lo tanto aqui los datos omitidos son **badchar**.
![[Pasted image 20251018182254.png]]

### Comparamos con mona
```shell
# Es lo que ejecutamos
# -f archivo.bin
# -a dirección hexadecimal
!mona compare -a 0x0231A128 -f C:\Users\chicoj2ck\Desktop\Analysis\bytearray.bin
```

### Resultado de comparación
![[Pasted image 20251018182740.png]]

### Generamos nuevamente el bytearrray sin los badchars
```shell
!mona bytearray -cpb "\x00\x0a"
```

### Resultado de repetidas ejecuciones de los pasos anteriores
![[Pasted image 20251018184559.png]]