___
- tags: #sqli #owasp 
___
## Que és?
Es una técnica de ataque utilizada para explotar vulnerabilidades en aplicaciones web que **no validan adecuadamente** la entrada del usuario en la consulta SQL que se envía a la base de datos.
## Inyecciones
Se produce cuando los atacantes insertan código SQL malicioso en los campos de entrada de una aplicación web.
### Inyección SQL basada en errores
Este tipo de inyección SQL aprovecha **errores en el código SQL** para obtener información.
### Inyección SQL basada en tiempo
Esta inyección utiliza una consulta que **que tarda mucho tiempo en ejecutarse** para obtener información.
### Inyección SQL basada en booleanos
Este tipo de inyección utiliza consultas con **expresiones booleanas** para obtener información adicional.
### Inyección SQL basada en uniones
Este tipo de inyecciones utiliza la cláusula **"UNION"** para combinar dos o más consultas en una sola.
### Inyección SQL basada en stacked queries
Este tipo de inyección aprovecha la posibilidad de **ejecutar múltiples consultas** en una sola sentencia para obtener información adicional.

## Tipos de DB
### Bases de datos relacionales
Las inyecciones SQL son más comunes en bases de datos relacionales como MySQL, SQL Server, Oracle, PostgreSQL, entre otros. En estas bases de datos, se utilizan consultas SQL para acceder a los datos y realizar operaciones en la base de datos.
### Bases de datos NoSQL
Aunque las inyecciones SQL son menos comunes en bases de datos NoSQL, todavía es posible realizar este tipo de ataque.
Las bases de datos NoSQL, como MongoDB o Cassandra, no utilizan el lenguaje SQL, sino un modelo de datos diferentes. Sin embargo, es posible realizar inyecciones de comandos en las consultas que se realizan en estas bases de datos.
### Bases de datos de grafos
Las bases de datos de grafos, como Neo4j, también pueden ser vulnerables a inyecciones SQL. En estas bases de datos, se utilizan consultas para acceder a los objetos que se han almacenado en la base de datos.
### Bases de datos de objetos
Las bases de datos de objetos, como db4o, también pueden ser vulnerables a inyecciones SQL. En estas bases de datos, se utilizan consultas para acceder a los objetos que se han almacenado en la base de datos.