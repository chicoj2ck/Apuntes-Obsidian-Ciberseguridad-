___
- tags: #prototype_pollution #owasp 
___
Es una técnica de ataque que aprovecha las vulnerabilidades en la implementación de JavaScript. Esta técnica de ataque se utiliza para modificar la propiedad "prototype" de un objeto en una aplicación web, lo que puede permitir al atacante ejecutar código malicioso o manipular los datos de la aplicación.

```json
# example
{
	"email":"wua@wua.com",
	"msg":"Mensaje para wua",
	"__proto__":{
		"admin":true
	}
}
```
