___
- tags: #sqli 
___
## What is a Database?
A database is a way of electronically storing collections of data in an organised manner.
### DBMS
 A database is controlled by a DBMS, which is an acronym for  Database Management System.
### What are tables?
A table is made up of columns and rows.
## Relational Vs Non-Relational Databases

### Relational
Relational database store information in tables, and often, the tables share information between them; they use columns to specify and define the data being stored and rows actually to store the data.

### Non-realtional
Non-relational databases, sometimes called NoSQL, on the other hand, are any sort of database that doesn't use tables, columns and rows to store the data. A specific database layout doesn't need to be constructed so each row of data can contain different information, giving more flexibility over a relational database.

## Select
The first query type we'll learn is the SELECT query used to retrieve data from the database.
```sql
select * from users;
```

### LIMIT
```sql
-- -limit 1
-- limita a 1 el resultado
select * from users limit 1;

-- -limit 1,1
-- limita a 1 el resultado y se salta una fila
select * from users limit 1,1;
```

### LIKE
Allows you to specify data that isn't an exact match but instead either starts, contains or ends with certain characters by choosing where to place the wildcard character represented by a percentage sign %.
```sql

-- - like '%n'
-- -  return rows with a username beginning with the letter a
select * from users where username like 'a%';
```

```sql

-- - like '%n'
-- -  return rows with a username ending with the letter n
select * from users where username like '%n';
```

```sql

-- - like '%mi%'
-- -  return rows with a username contain the characters mi within them.
select * from users where username like '%mi%';
```
 
### UNION
The UNION statement comines the results of two or more SELECT statements to retrieve data from either single or multiple tables.
 ```sql
 select name, address, city, postcode from customers UNION SELECT company, address, city, postcode from suppliers;
 ```

### INSERT
Tells database we wish insert a new row of data into the table. **"into users"** tells the database which table we wish to insert the data into, **"(username,password)"** provides the columns we are providing data for and then **"values('name','pass');"** provides the data for the previously specified columns.
```sql
insert into users (username, password) values ('name_test','pass123');
```
