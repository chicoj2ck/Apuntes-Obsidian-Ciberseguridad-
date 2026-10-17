___
- tags: #material_adicional #metasploit
___
## Que es
Es una plataforma de pruebas de penetración (**Penetration Testing Framework**) que se utiliza para realizar pruebas de seguridad en sistemas y aplicaciones.

```shell
# metasploit ejecuta metasploit
msfdb run

# ruta de archivos metasploit
/usr/share/metasploit-framework/modules/
```

## Comandos útiles
```shell
# Busca por plataforma o sistema operativo
search plataform:"windows"

# busca por tipo de script
seach plataform:"windows" type:"encoders"

# Usar script
use <script_path>

# muestra como se configura o que necesita
show options

# muestra más opciones
show advanced options

# muestra en aquel espacio de trabajo
hosts

# importa la información extraida desde nmap 
db_import /home/chicoj2ck/Desktop/chicoj2ck/machines/windows_sml/allPorts

# Mustra los distintos servicios detectados 
services

# Verifica si el objetivo es vulnerable
check

# Nos da la lista de sesiones activas
sessions
```