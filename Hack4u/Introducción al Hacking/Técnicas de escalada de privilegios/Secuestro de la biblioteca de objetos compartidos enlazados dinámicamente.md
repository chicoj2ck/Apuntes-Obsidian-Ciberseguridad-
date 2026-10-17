___
- tags: #abusing_privilege #library
___
## Bibliotecas Compartidas
Son archivos que contienen funciones y recursos utilizados por múltiples programas.
Cuando un programa requiere una función de una biblioteca compartida, el sistema operativo busca la biblioteca y enlaza dinámicamente la función requerida durante la ejecución del programa
## Perspectiva del atacante
Un atacante puede aprovechar esta situación creando una **biblioteca compartida maliciosa** con el mismo nombre que la biblioteca legítima y colocándola en un directorio donde el sistema la buscará.

## Enlazador dinámico
Carga por detrás las bibliotecas compartidas para que los programas funcionen
Toma como prioritario la variable de entorno **'LD_PRELOAD'**.
```shell
gcc -shared -fPIC test.c -o test
```

____
## Referencias
- [uftrace - Github](https://github.com/namhyung/uftrace).
- [Attack Defense Plataform](https://attackdefense.com/).