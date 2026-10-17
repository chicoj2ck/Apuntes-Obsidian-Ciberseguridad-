___
- tags: #deserializacion #owasp 
___
Los ataques de deserialización son un tipo de ataque que aprovecha las vulnerabilidades en los procesos de serialización y deserialización de objetos en aplicaciones que utilizan POO

## Serialización y Deserialización
La serialización es el proceso de convertir un objeto en una secuencia de bytes que puede ser almacenada o transmitida a través de una red. La deserialización es el proceso inverso, en el que una secuencia de bytes es convertida de nuevo a un objeto.
## Ataque 
Los ataques de deserialización pueden ocurrir en diferentes tipos de aplicaciones, incluyendo aplicaciones web, entre otros.
Estos ataques pueden ser explotados de varias maneras, como:
- Modificar el objeto serializado antes de que sea enviado a la aplicación, lo que puede causar errores en la deserialización y permitir que un atacante ejecute código malicioso.
- Enviar un objeto serializado malicioso que aproveche una vulnerabilidad en la aplicación para ejecutar código malicioso.
- Enviar un objeto serializado malicioso que aproveche una vulnerabilidad en la aplicación para ejecutar código malicioso.
- Realizar un ataque de "man-in-the-middle" para interceptar y modificar el objeto serializado antes de que llegue a la aplicación