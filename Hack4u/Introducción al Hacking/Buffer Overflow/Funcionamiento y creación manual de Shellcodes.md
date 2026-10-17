___
- tags: #buffer_overflow #shell_code  
___
 Los **shellcodes** son programas pequeños y altamente optimizados que se utilizan para explotar vulnerabilidades de seguridad y ejecutar código malicioso en una máquina objetivo. Los **shellcodes** suelen ser escritos en lenguaje **ensamblador** para garantizar rápida y eficiente.
 
## Ejemplo
Por ejemplo, intentaremos crear un shellcode que muestre por consola el mensaje “**Hola mundo**” utilizando interrupciones del sistema. Asimismo, intentaremos aplicar una llamada a nivel de sistema para lograr ejecutar un comando deseado.

Una vez que se ha generado el compilado resultante, se puede utilizar el comando **objdump** para convertir el archivo binario generado en un shellcode que pueda ser utilizado en un Buffer Overflow.

## Creación de binario
```shell
msfvenom -p linux/x86/exec CMD="echo 'Hola mundo'" -f elf -o binary
```

```shell
chmod +x binary
```

```shell
msfvenom -p linux/x86/exec CMD="echo 'Hola mundo'" -f raw | ndisasm -b32 -
```

