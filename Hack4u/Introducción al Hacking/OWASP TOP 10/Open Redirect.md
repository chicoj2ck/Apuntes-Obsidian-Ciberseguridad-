___
- tags: #owasp #open_redirect
___
La vulnerabilidad de redirección abierta, también conocida como **Open Redirect**, es una vulnerabilidad común en aplicaciones web que se puede ser explotada por los atacantes para dirigir a los usuarios a sitios web maliciosos.

### Bypass de filtro de '.'
```burp
/redirect?newurl=https://google%25%2ees
```

### Bypass de filtro de '/' y '.'
En dominios https, puedo omitir la doble barra ("//")
```burp
/redirect?newurl=https:google%25%2ees
```