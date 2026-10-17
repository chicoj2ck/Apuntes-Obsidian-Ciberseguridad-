___
- tags: #abusing_privilege #path_hijacking
____
**PATH Hijacking** es una técnica utilizada por los atacantes para **secuestrar** **comandos** de un sistema Unix/Linux mediante la manipulación del **PATH**. 
## Path
El PATH es una variable de entorno que define las rutas de búsqueda para los archivos ejecutables en el sistema.

Si un atacante es capaz de alterar el PATH y crear un nuevo archivo con el mismo nombre de uno de los comandos definidos internamente en el binario, puede lograr que el binario ejecute la versión maliciosa del comando en lugar de la versión legítima.