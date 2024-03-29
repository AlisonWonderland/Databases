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

PRIMARY KEY FOR TO LIMIT ENTRIES TO UNIQUE COMBINATIONS:
```sql
CREATE TABLE likes (
    user_id INT NOT NULL,
    photo_id INT NOT NULL,
    created_at TIMESTAMP DEFAULT NOW(),
    FOREIGN KEY(user_id) REFERENCES users(id),
    FOREIGN KEY(photo_id) REFERENCES photos(id),
    PRIMARY KEY(user_id, photo_id) --Means that the user_id and photo_id must be UNIQUE to be entered. The combo will can only happen/                                      --appear once in the table
);
```

FOREIGN KEY:
```sql
CREATE TABLE tablename
(
    colA INT,
    FOREIGN KEY(colA) REFERENCES other_table(other_table_col_name)
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

WHERE col_name LIKE '%\%%'
WHERE col_name LIKE '%\_%'
```
Note: Second one will search for data that starts with 'da'. Third one will search for data with the same amount of characters as the amount of underscores, in this example its 4 underscores so it will look for data that is 4 characters long. LIKE is used for better searching. The percentage symbols are called wildcards, they mean anything before and anything after respectively. CASE INSENSITIVE.


HAVING(used with GROUP BY instead of WHERE):
```sql
HAVING col_name = val;
```


<p align="center">
 <b>---------------------------AGGREGATE FUNCTIONS----------------------------</b><br>
</p>

To count entries in a table:
```sql
SELECT COUNT(optional: DISTINCT. col1_name, col2_name or *) FROM table_name;

SELECT COUNT(*) FROM table_name WHERE col_name LIKE '%%'; 
```
Note: (DISTINCT col1, col2) would return the number of rows with distinct combined values. Second line is to show that you can use COUNT() with LIKE.


To combine identical data into single rows:
```sql
SELECT col1,col2... aggregate_function() FROM table_name GROUP BY col1col2..;
```
Note: This is a confusing one to explain. As usual chaining columns after GROUP BY will give back unique results(think first name and last name). Use ANY_VALUE() around columns that are not mentioned in GROUP BY to remove error.


MIN and MAX:
```sql
SELECT MIN(col) FROM table_name;

SELECT MAX(col) FROM table_name;

SELECT * FROM books WHERE pages = (SELECT MIN(pages) FROM books);

SELECT * FROM books ORDER BY pages LIMIT 1;
```
Note: Third one will give you the row of the book with the smallest amount of pages. Third one uses sub queries, meaning two queries are happening at once. 4th does the same as the 3rd but is fastest.


To get the SUM of all the data in a row:
```sql
SELECT author, SUM(pages) FROM books GROUP BY author;
```

To get the AVG of all the data in a row:
```sql
SELECT author, AVG(pages) FROM books GROUP BY author;
```

<p align="center">
 <b>---------------------------TIME RELATED INFO----------------------------</b><br>
</p>
For data types go to: https://dev.mysql.com/doc/refman/8.0/en/date-and-time-types.html
For functions that work with the data types go to: https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html

<p align="center">
 <b>---------------------------LOGICAL OPERATORS----------------------------</b><br>
</p>

Equality operator: =

To not include certain data:
```sql
WHERE col NOT LIKE val;
WHERE col != val;
```

Using Greater than/equal sign:
```sql
WHERE col > val;
WHERE col >= val;
```

Using less than/equal sign:
```sql
WHERE col < val;
WHERE col <= val;
```

AND:
```sql
WHERE col < val AND col = "some_val";
WHERE col < val && col = "some_val";
```
NOTE: we can chain more than two expressions with AND.


OR:
```sql
WHERE col < val OR col = "some_val";
WHERE col < val || col = "some_val";
```
NOTE: we can chain more than two expressions with OR.


NOT/BETWEEN. To get data within a certain upper and lower range:
```sql
SELECT... WHERE price BETWEEN val1 AND val2;
SELECT... WHERE price NOT BETWEEN val1 AND val2;
```
NOTE: You can only use AND with BETWEEN, you can't use &&. Use cast to compare: https://dev.mysql.com/doc/refman/8.0/en/comparison-operators.html#operator_between .INCLUSIVE. 


NOT/IN. Used when OR would be used multiple times:
```sql
WHERE col_name IN ('val1', val2, 'val3');
WHERE col_name IN ('val1', val2, 'val3');
```
NOTE: NOT IN will bring back rows that don't include the values specified in the parentheses.

CASE STATEMENTS. Used similarly to if-else statements:
```sql
SELECT title, released_year,
 CASE
  WHEN released_year >= 2000 THEN 'Modern Lit'
  WHEN released_year < val THEN 'some_val'
  ELSE '20th Centrury Link'
 END AS GENRE
FROM books;
```
NOTE: THEN 'Modern Lit' means GENRE will be 'Modern Lit' if released_year >= 2000. When one WHEN statement is true, no other WHEN statements plus ELSE are used/checked. Kind of like else-if.


IF-ELSE STATEMENTS:
```sql
IF(conditional_statement, if_val, else_val); optional: AS
```
NOTE: Only use it when you have two values you want assigned based on a conditional statement, otherwise use CASE. When the conditional statement is true then the if_val statement is used, else the else_val is used for the row value.


<p align="center">
 <b>---------------------------JOINS----------------------------</b><br>
</p>

INNER JOIN:
```sql
SELECT * FROM table
JOIN table2
 ON table.id = table2.table_id;
 
SELECT * FROM table
INNER JOIN table2
 ON table.id = table2.table_id;
```
NOTE: In the ON portion we want to equal the primary and foreign key. In other words, we want to join where the two keys equal each other and ignore all rows where the two values don't match.


LEFT JOIN:
```sql
SELECT * FROM table
LEFT JOIN table2
 ON table.id = table2.table_id;
```

RIGHT JOIN:
```sql
SELECT * FROM table
RIGHT JOIN table2
 ON table.id = table2.table_id;
```

ON DELETE CASCADE:
```sql
CREATE TABLE orders(
    id INT AUTO_INCREMENT PRIMARY KEY,
    order_date DATE,
    amount DECIMAL(8,2),
    customer_id INT,
    FOREIGN KEY(customer_id) 
        REFERENCES customers(id)
        ON DELETE CASCADE
);
```
NOTE: Key words to add in CREATE TABLE to delete any rows in the child table containing the foreign key of the rows deleted in the parent table.


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

MODULO
```
%
```

IFNULL:
```sql
IFNULL(col_val_you_want_to_check, replacement_val);

IFNULL(SUM(amount), 0) AS total_spent; 
```
NOTE: Checks if a value is null and replaces it. If a value isn't null then that value will appear.


IS NULL:
```sql
SELECT *
FROM table_name
WHERE col.val IS NULL
```
NOTE: This will return all rows where col.val is null. Is null is self explanatory, it checks if a value is null.


ROUND:
```sql
ROUND(
 AVG(col_val),
 2
) AS rounded_avg
```
NOTE: Functions that rounds. Takes in the column you want to round and how many numbers you want after the decimal point. In this case the average will get round to two digits after the decimal point.
Examples:
If average is 7.8624 then after Round() it will be 7.86.
If average is 123.24 then after Round() it will be 123.24.


## Additional Notes
* Usernames are a good example of a primary key when you don't want them to be duplicated. That way you can use the error in mySQL and pass it back to the user. 
* CRUD are the four main operations that we will use on our data.
* WHERE is by default case insensitive for val.
* Primary keys won't/shouldn't change when rows are deleted because other tables might use those keys. Updating them can obviously cause issues.
* Pagination is an interesting concept.
* When to use TIMESTAMP and DATETIME: Timestamps are used for meta date, when things are created or updated.
* DATETIME has a larger date range, while also being 2 time bigger.
* <b> Big note </b> 'a' = 'A'.
* NEED TO KNOW SELF JOINS
