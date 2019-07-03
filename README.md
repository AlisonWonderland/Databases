# Databases

## Commands to use in WSL
* sudo service mysql start
* sudo mysql -u root. <-- To enter mysql command line.

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

To create table(w/ NOT NULL as well): 
```sql
CREATE TABLE tablename
 (
  column_name data_type,
  column_name data_type
 );
 
CREATE TABLE tablename
(
  column_name data_type NOT NULL,
  column_name data_type NOT NULL
);

-------SETTING DEFAULTS--------
CREATE TABLE tablename
(
  column_name data_type DEFAULT def_val,
  column_name data_type NOT NULL DEFAULT def_val
);
```
NOT NULL means that an empty value shouldn't be inserted, will give a warning message if this happens. Meaning a default value must be specified. 
Line will not allow a NULL value to be inserted. Important to prevent people from passing NULL for an INT value.

Setting up a table with a primary key(a unique identifier for each row):
```sql
CREATE TABLE tablename
(
  id INT NOT NULL,
  column_name data_type DEFAULT def_val,
  PRIMARY KEY (id)
);
```

Setting up a table with an auto incrementing primary key:
```sql
CREATE TABLE tablename
(
  id INT NOT NULL AUTO_INCREMENT,
  column_name data_type DEFAULT def_val,
  PRIMARY KEY (id)
 
  -----or-----
  id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  column_name data_type DEFAULT def_val,
);
```

To print out all tables in a database:
```sql
SHOW TABLES;
```
To print out columns of a table(slight difference between the two):
```sql
SHOW COLUMNS FROM/IN table_name;
DESC table_name;
```
To delete/drop table:
```sql
DROP TABLE table_name;
```

Inserting data into our tables. col2 can come before col1, but val2 would have to be switched with val1. Commas separate different row entry values.:
```sql
INSERT INTO table_name(column1_name, column2_name)
VALUES (val1, val2)
      ,(val3, val4);
      
--------for one row:---------
INSERT INTO table_name(column1_name, column2_name) VALUES (val1, val2);

--------for one value in a column:---------
INSERT INTO table_name(column1_name) VALUES (val1);
```

---------------------------------MESSAGE RELATED COMMANDS----------------------------------------
To see what the warnings are:
```sql
SHOW WARNINGS;
```

## Additional Notes
* Usernames are a good example of a primary key when you don't want them to be duplicated. That way you can use the error in mySQL and pass it back to the user. 
* CRUD are the four main operations that we will use on our data.
