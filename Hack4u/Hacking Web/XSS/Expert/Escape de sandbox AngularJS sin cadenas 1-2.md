----
- Tags: #xss #owasp #angular #portswigger 
---

## Sandbox
Es una forma de angular de sanitizar los 
## Enfoque
La idea es utilizar funciones nativas de javascript para construir cadenas de forma indirecta.
## Paso a paso

### Obtenemos la versión de angular

```javascript
angular.version.full
// response from console ->"1.4.4" 
```

### Métodos
Utilizamos el método 'toString()' y la propiedad 'constructor' para acceder al prototipo de  los objetos y redefinir como se comportan.

### Finalmente

al ver que la función tiene una evaluación previa de lo que se busca, nos permite que se interprete código en la función **$parse**.

```txt
https://0a3b004603642be880ff03cb005c00ed.web-security-academy.net/?search=wua&2%2B7

#-> como resultasdo nos da 9
```

Por lo tanto filtramos por la versión **1.4.4** para buscar como escapar/romper el Sandbox
[PortSwigger - xss - cheat - sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet#angularjs-sandbox-escapes-reflected)

### Arreglo
no evaluar con **$parse** como valor aparte ...