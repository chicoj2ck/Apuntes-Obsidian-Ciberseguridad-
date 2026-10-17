___
- tags: #index #buffer_overflow
___
## Que es Buffer Overflow...
Es una vulnerabilidad común en software que puede permitir a un atacante ejecutar código malicioso o tomar control de un sistema comprometido

Esta vulnerabilidad se produce cuando un programa intenta almacenar más datos en un **búfer** (zona de memoria temporal para almacenar datos) de lo que se había previsto, y al exceder la capacidad del búfer, los datos adicionales se escriben en otras zonas de memoria adyacentes.

## Indice
1. [[Creación de nuestro laboratorio de pruebas e instalación de Immunity Debuger]].
2. [[Fase inicial de Fuzzing y tomando el control del registro EIP]].
3. [[Asignación de espacio para el Shellcode]].
4. [[Generación de Bytearrays y detección de Badchars]].
5. [[Búsqueda de OpCodes para entrar al ESP y cargar nuestro Shellcode]].
6. [[Uso de NOPs, desplazamientos en pila e interpretación del Shellcode para lograr RCE]].
7. [[Modificación del Shellcode para controlar el comando que se desea ejecutar]].