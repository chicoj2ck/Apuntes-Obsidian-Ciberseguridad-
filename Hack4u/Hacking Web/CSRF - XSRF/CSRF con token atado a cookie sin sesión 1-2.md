___
- tags: #csrf #xsrf 
___
Vemos que requiere ser válido el csrf token con la cookie csrfKey, so requerimos que coincidan al intentar enviarlo por el servidor atacante.

Aprovechamos que se setea la búsqueda como cookie e inyectamos nuevas cookies:
```txt
SameSite=None
```
Esta cookie es necesaria para decirle al navegador que cruce las cookies al cambiar de sitio (por la url del servidor atacante).