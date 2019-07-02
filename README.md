# Databases

## Commands to use in WSL
* sudo service mysql start
* sudo mysql -u root. To enter mysql

## SQL Commands
<p align="center">
 <b>-------------------------DATABASE CREATION RELATED COMMANDS--------------------</b><br>
</p>

* CREATE DATABASE < database name > Creates new database. Don't include <>.
* DROP DATABASE < database name >; Deletes database.
* USE < database name >; Switches to new database so that you can use it.
* SELECT database(); Gives you the name of the database you're currently using. May be the NULL database, which is the "starting" database.
* SHOW DATABASES; Prints out names of all databases.

<p align="center">
 <b>---------------------------DATABASE TABLE RELATED COMMANDS----------------------------</b><br>
</p>

To create table: 
```sql
CREATE TABLE tablename
 (
  column_name data_type,
  column_name data_type
 );
```
To print out all tables in a database:
```sql
SHOW TABLES;
```
To print out columns of a table(slight difference between the two):
```sql
SHOW COLUMNS FROM table_name;
DESC table_name;
```
To delete/drop table:
```sql
DROP TABLE table_name;
```

Inserting data into our tables. col2 can come before col1, but val2 would have to be switched with val1. Commas separate different row entry values.:
```
INSERT INTO table_name(column1_name, column2_name)
VALUES (val1, val2)
      ,(val3, val4);
```
