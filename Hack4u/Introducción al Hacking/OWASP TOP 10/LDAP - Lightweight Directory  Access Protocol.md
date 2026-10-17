___
- tags: #ldap #owasp 
___
Las inyecciones LDAP son un tipo de ataque en el que se aprovechan las vulnerabilidades en las aplicaciones web que se interactúan con un servidor LDAP.
## Servidor LDAP
Directorio que se utiliza para almacenar información de usuarios y recursos en una red.

```shell
ldapsearch -x -H ldap://localhost -b dc=example, dc=org -D "cn=admin, dc=example, dc=org" -w admin
```

## Inyección
```txt
username=admin))%00
```

