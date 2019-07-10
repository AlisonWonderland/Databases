# Databases

## Commands to start up mysql in WSL
* sudo service mysql start
* sudo mysql -u root. <-- To enter mysql command line.

## How to install mysql
Use: https://medium.com/@fiqriismail/how-to-setup-apache-mysql-and-php-in-linux-subsystem-for-windows-10-e03e67afe6ee
But, for one part you need to look in the comments. When it doesn't ask for a password in the installation.

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

<p align="center">
 <b>---------------------------MESSAGE RELATED COMMANDS----------------------------</b><br>
</p>

To see what the warnings are:
```sql
SHOW WARNINGS;
```

<p align="center">
 <b>---------------------------READING DATA COMMANDS----------------------------</b><br>
</p>

To get data from all columns:
```sql
SELECT * FROM table_name;
```

To get data from a specific column:
```sql
SELECT column_name FROM table_name;
```

To get data from multiple columns:
```sql
SELECT column_name1, column_name2,3,4.. FROM table_name;
```

To get rows that have a certain value for a column:
```sql
SELECT column_name or * FROM table_name WHERE column_name=val_u_want;
```

<p align="center">
 <b>---------------------------UPDATING DATA COMMANDS----------------------------</b><br>
</p>

Updating all instances of a value in a column:
```sql
UPDATE table_name SET col_name='new_val' or #, col2_name....
WHERE col_name='old_val' or #
```
Good rule of thumb: Try selecting the data/row of data you want to change so that you can check that your WHERE condition gives you the right data to change.

<p align="center">
 <b>---------------------------DELETING DATA COMMANDS----------------------------</b><br>
</p>

Deleting all instances/row with a column value of val:
```sql
DELETE FROM table_name WHERE col_name='val' or #
```

Deleting all data/rows in a table(doesn't delete table):
```sql
DELETE FROM table_name;
```

<p align="center">
 <b>---------------------------RUNNING SQL FILES COMMANDS----------------------------</b><br>
</p>

To run file in current directory:
```sql
source file_name.sql
```

To run file in a nested directory:
```sql
source /../parent_folder/folder_file_is_in file_name.sql
```
Note: You can't run files in another folder that isn't in the parent folder.

<p align="center">
 <b>---------------------------STRING FUNCTIONS----------------------------</b><br>
</p>

To combine # of columns:
```sql
SELECT
 CONCAT(col1, 'text', col2,...,col5,...) optional: AS 'alias'
FROM table_name;
```
Note: 'text' is optional. You can add it when you want something in between the values of the combined columns.
Also, CONCAT won't add the concated column to the table.

To combine # of columns w/ the same separator between them:
```sql
SELECT
 CONCAT_WS('-', col1, col2,...,col5,...); optional: AS 'alias'
FROM table_name;
```
Note: This will create a table where the column data will be separated by '-'

Getting a substring:
```sql
SUBSTRING('string', start_index, last_index)

or

SUBSTRING('string', start_index)

or 

SUBSTR()
```
Note: Indicies start at 1. Second one will give you the substring from start_index to the last character.

To replace parts of a string:
```sql
SELECT REPLACE('string_that_needs_change', 'substring_that_will_change', 'replacement_substr');
```

To reverse string:
```sql
SELECT REVERSE('string' or col_name); optional: AS, FROM table (if you use col_name)
```

To get number of characters in a string:
```sql
SELECT CHAR_LENGTH('string' or col_name); optional: AS, FROM table (if you use col_name)
```

To lower/upper case a sub/string:
```sql
SELECT LOWER/UPPER('string' or col_name); optional: AS, FROM table (if you use col_name)
```

<p align="center">
 <b>---------------------------REFINING SELECTION COMMANDS----------------------------</b><br>
</p>

To get distinct values:
```sql
SELECT DISTINCT col_name FROM table_name;
```
Note: Separating multiple col_names with commas will give you back unique rows, i.e it will give you the same result if you used DISTINCT CONCAT(). 

To sort data:
```sql
SELECT col_name FROM table_name ORDER BY col_name;

SELECT col_name FROM table_name ORDER BY col_name DESC;

SELECT col1_name, col2_name, col3_name FROM table_name ORDER BY 2;  optional: DESC

SELECT col1_name, col2_name, col3_name FROM table_name ORDER BY col1_name, col2_name;  optional: DESC
```
Note: This will sort in ascending order by defualt. Use second one for descending order. Third one will sort the table by the second col(col2_name). Its a short hand method. 4th one will order by col1 and then order by col2. ORDER BY is alpha-numeric.

To limit data printed/recieved:
```sql
SELECT col_name FROM table_name LIMIT 2;

SELECT col_name FROM table_name LIMIT 0,2;
```
Note: This example will give you the first 2 rows of the column from the table. Second example will start the first row(represent by 0) and go for 2 rows. So it will give us the first 2 rows. Usually used with ORDER BY. 

To get data containing the string between the wildcards:
```sql
WHERE col_name LIKE '%da%'

WHERE col_name LIKE 'da%'

WHERE col_name LIKE '____'
```
Note: Second one will search for data that starts with 'da'. Third one will search for data with the same amount of characters as the amount of underscores, in this example its 4 underscores so it will look for data that is 4 characters long. LIKE is used for better searching. The percentage symbols are called wildcards. CASE INSENSITIVE.

<p align="center">
 <b>---------------------------MISC COMMANDS----------------------------</b><br>
</p>

Aliases(useful when joining tables and columns have the same name):
```sql
SELECT column_name AS new_name FROM table_name;
```
Note: You can write the alias/new_name with single quotes('') around to include spaces. EX: 

```sql
SELECT cat_breed AS 'cat breed' FROM table_name;
```

## Additional Notes
* Usernames are a good example of a primary key when you don't want them to be duplicated. That way you can use the error in mySQL and pass it back to the user. 
* CRUD are the four main operations that we will use on our data.
* WHERE is by default case insensitive for val.
* Primary keys won't/shouldn't change when rows are deleted because other tables might use those keys. Updating them can obviously cause issues.
* Pagination is an interesting concept.
