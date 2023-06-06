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

According to those steps we should create a **table** called *"Cities"* containing **columns** called *"name", "country", "population"* and *"area"*. Each column should indicate the type of data that it is going to store.

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
## 
