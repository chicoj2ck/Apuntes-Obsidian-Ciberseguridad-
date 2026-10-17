___
- tags: #buffer_overflow #esp
___
## ESP - Extended Stack Pointer
 Es un registro de la CPU que se utiliza para manejar la pila (**stack**) en un programa. La pila es una zona de memoria temporal que se utiliza para almacenar valores y **direcciones de retorno** de las funciones a medida que se van llamando en el programa.
## Que sigue
Una vez que se ha identificado la ubicación de los caracteres en la memoria, la idea principal en este punto es introducir un **shellcode** en esa ubicación, que son instrucciones de bajo nivel las cuales en este caso corresponderán a una instrucción maliciosa.

Hay que hacer que el **EIP** apunte a una dirección que permita hacer un **salto al ESP** 