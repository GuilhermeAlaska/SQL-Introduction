# Types most used in SQL:

- Integer
- Text
- Date
- Real

> Statement always end up with a " ; ">

CREATE TABLE creates a new table.
INSERT INTO adds a new row to a table.
SELECT queries data from a table.
ALTER TABLE changes an existing table.
UPDATE edits a row in a table.
DELETE FROM deletes rows from a table.
----------------------------------------------------------------
SELECT is the clause we use every time we want to query information from a database.
AS renames a column or table.
DISTINCT return unique values.
WHERE is a popular command that lets you filter the results of the query based on conditions that you specify.
LIKE and BETWEEN are special operators.
AND and OR combines multiple conditions.
ORDER BY sorts the result.
LIMIT specifies the maximum number of rows that the query will return.
CASE creates different outputs.


COUNT(): count the number of rows
SUM(): the sum of the values in a column
MAX()/MIN(): the largest/smallest value
AVG(): the average of the values in a column
ROUND(): round the values in the column


----------------------------------------------------------------
SELECT * FROM 'table' >> Use to select a specific table
SELECT name, genre, year FROM movies; >> You can select a specific column in the table
SELECT imdb_rating AS 'IMDb' FROM movies; >> You can rename a column in the table
SELECT DISTINCT genre FROM movies; >> Select distinct items from the table

SELECT * FROM movies
WHERE imdb_rating < 5; >> Select only those who have a rating less than 5 / Can be used math operators (>, <, <=>)

SELECT * FROM movies
WHERE name LIKE 'Se_en'; >> like is a special keyword to search for a determined value, and _ is any other value
WHERE name LIKE '%man%'; >> % is also a special keyword to search for 'man', to the right search for A'any' and before 'any'A 
WHERE imdb_rating IS NULL; >> Only show the rows that are null 

SELECT * FROM movies >> Select all information
WHERE name >> from name 
BETWEEN 'D' AND 'G'; >> G will not be show

SELECT * FROM movies
WHERE year 
BETWEEN 1970 AND 1979; >> Also includes 79'
BETWEEN 1970 AND 1979 AND imdb_rating > 8; >> You can declare more info about what you want to be show

SELECT * FROM movies
WHERE year < 1985 >> Only < 1985
AND genre = 'horror'; >> and if it's genre is 'horror'

WHERE year > 2014
OR genre = 'action'; >> OR brings the two results or, if one of them is empty, brings the second one only / AND brings only if the two of them are true or have values

SELECT name, year FROM movies >> takes the two methods
ORDER BY name; >> brings them in alphabetically order

SELECT name, year, imdb_rating FROM movies
ORDER BY imdb_rating DESC; >> Brings it descending order, only works with numbers

SELECT * FROM movies
WHERE imdb_rating
ORDER BY imdb_rating DESC
LIMIT 3; >> Limits the search to three items only

SELECT name,
  CASE
    WHEN genre = 'romance' THEN 'Chill'
    WHEN genre = 'comedy' THEN 'Chill'
    ELSE 'Intense'
 END AS 'MOOD' // Adds a new row for you to see the printed results
FROM movies;



CREATE TABLE 'table' (id INTEGER, name TEXT, age INTEGER); > Declaring the variables in database

INSERT INTO 'table' (id, name, age) VALUES (1, 'John',32); > Assigning the variables a value

SELECT name FROM celebs; >> select a specific column in the table

ALTER TABLE celebs >> To alter an existing table

ADD COLUMN twitter_handle TEXT; >> Is adding a column to the table
-
UPDATE celebs >> Command to update a existing row and column
SET twitter_handle = '@taylorswift13' >> setting the desired value
WHERE id = 4; >> What is the id of the row that'll be changed

DELETE FROM celebs >> Needless to say
WHERE twitter_handle IS NULL; >> Where you want to delete / It deleted all the rows where twitter_handle were NULL




CREATE TABLE celebs (
   id INTEGER PRIMARY KEY, 
   name TEXT UNIQUE,
   date_of_birth TEXT NOT NULL,
   date_of_death TEXT DEFAULT 'Not Applicable'
);

1. PRIMARY KEY columns can be used to uniquely identify the row. Attempts to insert a row with an identical value to a row already in the table will result in a constraint violation which will not allow you to insert the new row.

2. UNIQUE columns have a different value for every row. This is similar to PRIMARY KEY except a table can have many different UNIQUE columns.

3. NOT NULL columns must have a value. Attempts to insert a row without a value for a NOT NULL column will result in a constraint violation and the new row will not be inserted.

4. DEFAULT columns take an additional argument that will be the assumed value for an inserted row if the new row does not specify a value for that column.



COUNT(): count the number of rows
SELECT COUNT(*) FROM fake_apps >> Shows how many rows are in total
WHERE price = 0; >> Givin it a parameter, to search only for those who are free

SUM(): the sum of the values in a column

SELECT SUM(downloads) >> It's summing all the values in the column downloads
FROM fake_apps;


MAX()/MIN(): the largest/smallest value
SELECT MIN(downloads) FROM fake_apps; // Show the least downloaded app
SELECT MAX(price) FROM fake_apps; // the most expensive app


AVG(): the average of the values in a column
SELECT AVG(downloads) from fake_apps;
SELECT AVG(price) from fake_apps;


ROUND(): round the values in the column
SELECT name, ROUND(price, 0) >> select the name, and round the prices to 0, so 2.8 would be 3.0
FROM fake_apps;

SELECT ROUND(AVG(price), 2) >> Takes the average of the value price and rounds it to 2 decimal houses
FROM fake_apps;

SELECT name, ROUND(price, 0) FROM fake_apps
WHERE price 
ORDER BY price DESC;

------------------------------------------------------------------------------------------------
GROUP BY 
The GROUP BY statement comes after any WHERE statements, but before ORDER BY or LIMIT.

SELECT price, COUNT(*) // is counting how many apps has more than 20000 downloads
FROM fake_apps
WHERE downloads > 20000
GROUP BY price;

SELECT category, SUM(downloads) >> is summing all the downloads of each category
FROM fake_apps
GROUP BY category; >> category of the apps

GROUP BY II

SELECT category, 
   price,
   AVG(downloads)
FROM fake_apps
GROUP BY 1, 2; >> It's grouping by the two columns previous defined (category, price) / category is being defined by it's name, and price it's being defined by least to most expensive

---------------------------------------------------------------
HAVING
When we want to limit the results of a query based on values of the individual rows, use WHERE.
When we want to limit the results of a query based on an aggregate property, use HAVING.

HAVING statement always comes after GROUP BY, but before ORDER BY and LIMIT.

SELECT price, 
   ROUND(AVG(downloads)),
   COUNT(*)
FROM fake_apps
GROUP BY price
HAVING COUNT(name) > 10; >> It's only showing those prices that has more than 10 apps(name)

