___
- tags: #owasp #session_puzzling
___
## Session Puzzling/ Session Fixation/ Session Variable
Vulnerabilidad de seguridad que afecta la **gestión de sesiones** en una aplicación web.
### Session Fixation
Se produce cuando un atacante establece un identificador de sesión válido para un usuario y luego espera a que el usuario inicie sesión. Si el usuario inicia sesión con el identificador de sesión, el atacante podría acceder a la sesión del usuario y realizar acciones maliciosas en su nombre.
### Session Puzzling
Se refiere refiere a la misma vulnerabilidad, pero desde el punto de vista del atacante que intenta **adivinar** o **generar identificadores** de sesión válidos.
### Session Variable Overloading
Se refiere a un tipo de ataque específico de Session Fixation en el que el atacante envía una gran cantidad de datos a la aplicación web con el objetivo de sobrecargar las variables de sesión.