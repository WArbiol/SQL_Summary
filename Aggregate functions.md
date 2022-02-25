# AGGREGATE FUNCTIONS
Now, we are going to learn how to perform calculations using SQL.

Calculations performed on multiple rows of a table are called aggregates.

Quick preview of some important aggregates

- **COUNT()**: count the number of rows
- **SUM()**: the sum of the values in a column
- **MAX()/MIN()**: the largest/smallest value
- **AVG()**: the average of the values in a column
- **ROUND()**: round the values in the column

## COUNT
**COUNT** is a function that **takes** the **name** of a **column** as an argument and counts the **number** of **non-empty** values **in** that **column**.
```
SELECT COUNT(*)
FROM fake_apps
WHERE price = 0;
```
## SUM
**SUM** is a function that takes the name of a column as an argument and returns the **sum** of **all** the **values in** that **column**.
```
SELECT SUM(downloads)
FROM fake_apps;
```

## MAX / MIN
The **MAX** and **MIN** functions return the **highest** and **lowest** values in a **column**, respectively.

How many downloads does the most popular app have?
```
SELECT MAX(downloads)
FROM fake_apps;
```
## AVERAGE
AVG() function to quickly calculate the average value of a particular column.  

How much is the average number of downloads for an app in our database?
```
SELECT AVG(downloads)
FROM fake_apps;
```
## ROUND
By default, SQL tries to be as precise as possible without rounding. We can make the result table **easier to read** using the ROUND() function.

ROUND() function takes two arguments inside the parenthesis:

1. A **column name**
2. An **integer**, the number of decimal places
```
SELECT name, ROUND(price, 0)
FROM fake_apps;
```
Now rounding the average price to two decimal places:
```
SELECT ROUND(AVG(price), 2)
FROM fake_apps;
```
## GROUP BY
If we want to know the mean IMDb ratings for all movies each year we can group the output by the year:
```
SELECT year,
   AVG(imdb_rating)
FROM movies
GROUP BY year
ORDER BY year;
```
The **GROUP BY** statement comes **after** any **WHERE** statements, but **before** **ORDER BY** or **LIMIT**. Example:
```
SELECT price, COUNT(*)
FROM fake_apps
WHERE downloads > 20000
GROUP BY price
ORDER BY price DESC;
```
### **Column references**
If we want to know how many movies have IMDb that round to 1, 2, 3, 4, 5. We could do this:
```
SELECT ROUND(imdb_rating),
   COUNT(name)
FROM movies
GROUP BY ROUND(imdb_rating)
ORDER BY ROUND(imdb_rating);
```
It's time-consuming to write and prone to error. 

So we can use **column references**:
- 1 is the first column selected
- 2 is the second column selected
- 3 is the third column selected
```
SELECT ROUND(imdb_rating),
   COUNT(name)
FROM movies
GROUP BY 1
ORDER BY 1;
```
Here "1" refers to the first column, ROUND(imdb_rating) and "2" would refers to the COUNT(name) column.

Another example with more than one group by:
```
SELECT category, 
   price,
   AVG(downloads)
FROM fake_apps
GROUP BY 1, 2;
```
## HAVING 
SQL also allows you to filter which groups to include and which to exclude.

Imagine that we want to see how many movies of different genres were produced each year, but we only care about years and genres with at least 10 movies.

We can’t use WHERE here because we don’t want to filter the rows; we want to **filter groups**.

**HAVING** is very **similar** to **WHERE**. In fact, all types of WHERE clauses you learned about thus far can be used with HAVING.

We can use the following for the problem:
```
SELECT year,
   genre,
   COUNT(name)
FROM movies
GROUP BY 1, 2
HAVING COUNT(name) > 10;
```
- When we want to limit the results of a query based on values of the **individual rows**, use **WHERE**.
- When we want to limit the results of a query based on an **aggregate property**, use **HAVING**.

**HAVING** statement always comes **after GROUP BY**, but **before ORDER BY** and **LIMIT**.

```
SELECT price, 
   ROUND(AVG(downloads)),
   COUNT(*)
FROM fake_apps
GROUP BY price
HAVING COUNT(*)>10;
```
Its query the price, downsload in this price, and number of apps, if the number of apps is greater than 10.

## REVIEW
- COUNT(): count the number of rows
- SUM(): the sum of the values in a column
- MAX()/MIN(): the largest/smallest value
- AVG(): the average of the values in a column
- ROUND(): round the values in the column

**Aggregate functions:**

- GROUP BY is a clause used with aggregate functions to combine data from one or more columns.
- HAVING limit the results of a query based on an aggregate property.