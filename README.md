# SQL Basics

## What is SQL?
SQL stands for *Structured Query Language*. It is a domain-specific language used to managing data held held in relational databases. It is supported by many different databases like MySQL, Microsoft SQL, Oracle.
Generally it is used to put information in database, to update it, read it and delete it. The most difficult from these four - and most complicated - is retrieving information.

## Storing a table in a database
### Table design process
When creating a table we need to answer ourselves for many questions. The most important are:
1. What kind of *thing* are we storing? **For example: we are storing the list of _cities_**
2. What properties does this *thing* have? **Each city has a _name_, _country_, _population_ and _area_**
3. What type of data does each of those properties contain? **name → _string_, country → _string_, population → _number_, area → _number_**

According to those steps we should create a **table** called *"cities"* containing **columns** called *"name", "country", "population"* and *"area"*. Each column should indicate the type of data that it is going to store.

### SQL Statement
SQL statement for creating the table mentioned in the previous section.
```
CREATE TABLE cities(
  name VARCHAR(50),
  country VARCHAR(50),
  population INTEGER,
  area INTEGER
);
```
### Inserting data into a table
When inserting the data we need to mention the table and optionally names of the columns. The order of mentioning the columns may be different to the one with which we initialized our table. Nonetheless the values for a specific record (row) need to be given in the same order as columns in a statement. We can

### SQL Statement
SQL statement for inserting data into previously created table "cities".

We can add just one row:
```
INSERT INTO cities (name, country, population, area)
VALUES ('Tokyo', 'Japan', 37732000, 8231);
```
or multiple rows:
```
INSERT INTO cities (name, country, population, area)
VALUES 
  ('Delhi', 'India', 32226000, 2344),
  ('Shanghai', 'China', 24073000, 4333),
  ('Sao Paulo', 'Brazil', 23086000, 3649);
```
If we won't give columns names we need to write values of a record in the same order as the table was created with.
```
INSERT INTO cities
VALUES 
  ('Mexico City', 'Mexico', 21804000, 2530);
```
If we won't write values for all of the columns, the columns for which the values weren't given will store "null".
```
INSERT INTO cities
VALUES 
  ('Cairo', 'Egypt');
```

Writing all of these statements will produce a table visualised below.
<br>CITIES:

| name | country | population | area |
| --- | --- | --- | --- |
| Tokyo | Japan | 37732000 | 8231 |
| Delhi | India | 32226000 | 2344 |
| Shanghai | China | 24073000 | 4333 |
| Sao Paulo | Brazil | 23086000 | 3649 |
| Mexico City | Mexico | 21804000 | 2530 |
| Cairo | Egypt | null | null |

## Retrieving data with SELECT
If we'd like to retrieve all of the data store in our table we can use asterisk which means "ALL" in SQL.
```
SELECT * FROM cities;
```
It will show us all of the columns with all of the records stored in the table "cities".
<br><br> We can also select just some of the columns:
```
SELECT country, name FROM cities;
```
This will show only two columns: country and name. They will be displayed in an order we write them in a statement.
<br> We can also select the same column multiple times (usefult when displaying lots of columns):
```
SELECT name, country, name FROM cities;
```
### Calculated columns
We can transform or proccess data before pulling it out from a database. We can work with different types of data.
<br><br>**NUMBERS**
<br>There are a few of math operations we can do on our record. 
<br> The basics are:

| SYMBOL | OPERATION |
| --- | --- |
| + | ADD |
| - | SUBTRACT |
| * | MULTIPLY |
| / | DIVIDE |
| ^ | EXPONENT |
| \|/ | SQUARE ROOT |
| @ | ABSOLUTE VALUE |
| % | REMAINDER |

<br>**STRINGS**
| SYMBOL | OPERATION |
| --- | --- |
| \|\| | Join two strings |
| CONCAT() | Join two strings |
| LOWER() | Gives a lowercase string |
| UPPER() | Gives an uppercase string |
| LENGTH() | Gives number of characters in a string |

<br>We can use this functions and operations in a SELECT statement to pull transformed data from our database.
<br><br> **EXAMPLES**
<br> To retrieve the density of population we need to divide population by area:
```
SELECT name, population/area AS population_density FROM cities;
```
To better understand the visualised data we can name the calculated column using alias with AS statement.
<br> To select the name and the country as a one string we can use both **||** or **CONCAT()**:
```
SELECT name || ', ' || country FROM countries;
```
or
```
SELECT CONCAT(name, ', ', country) FROM cities;
```
As we see, we can also add any string given between two single quotes.

## Filtering the data
The WHERE keyword allows us to filter the set of results we get back from a query. For example we want to see the cities which has the area over 4000 (square kilometers):
```
SELECT * FROM cities WHERE area > 4000;
```
Instead of ">" sign we can use a variety of comparison math operators:
| SYMBOL | OPERATION |
| --- | --- |
| = | Are the values equal? |
| > | Is the value on the left greater? |
| < | Is the value on the left smaller? |
| >= | Is the value on the left greater or equal to? |
| <= | Is the value on the left smaller or equal to? |
| <> or != | Are the values not equal? |
| IN | Is the value present in the list? |
| NOT IN | Is the value not present in the list? |
| BETWEEN | Is the value between two other values? |

Example for IN/NOT IN clause:
```
SELECT * FROM cities
WHERE name IN ('Tokio', 'Sao Paulo');
```
Example for BETWEEN clause:
```
SELECT * FROM cities
WHERE area BETWEEN 3000 AND 5000;
```
### Compound WHERE clauses
We can use several conditions to filter our records. To do so, we need to combine WHERE clause with AND, OR and NOT operators.
```
SELECT * FROM cities
WHERE area > 4000 AND country = 'China';
```
### Calculations in WHERE clause
It is also possible to do calculations like in SELECT clause. 
```
SELECT
  name,
  population/area AS population_density
FROM
  cities
WHERE
  population/area > 6000;
```
