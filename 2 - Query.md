# QUERIES
Fun fact: IBM started out SQL as SEQUEL (Structured English QUEry Language) in the 1970’s to query databases.

## SELECT
We can select individual columns by their names
```
SELECT column1, column2 
FROM table_name;
```
* FROM got moved to another line.
Line breaks don’t mean anything specific in SQL.

## AS
AS is a keyword in SQL that allows you to rename a column or table using an alias.  
It can be anything you want as long as you put it inside of single quotes
```
SELECT name AS 'Titles'
FROM movies;
```
* Although it’s not always necessary, it’s best practice to surround your aliases with single quotes.
* When using AS, the columns are not being renamed in the table. The aliases only appear in the result.

## DISTINCT
DISTINCT is used to return unique values in the output, filtering all duplicate values in the specified column(s).
```
SELECT DISTINCT tools 
FROM inventory;
```

## WHERE
Its used to restrict our query results in order to obtain only the information we want.
```
SELECT *
FROM movies
WHERE imdb_rating > 8;
```
1. **WHERE** clause **filters** the result set to only include rows where the following condition is **true**.
2. imdb_rating > 8 is the **condition**. Here, **only** rows with a value greater than 8 in the imdb_rating column will be **returned**.

Comparison **operators** used with the WHERE **clause** are:

* ``=`` equal to  
* ``!=`` not equal to  
* ``>`` greater than  
* ``<`` less than  
* ``>=`` greater than or equal to  
* ``<=`` less than or equal to

## LIKE 
LIKE can be a useful operator when you want to compare similar values.  
The movies table contains two films with similar titles, ‘Se7en’ and ‘Seven’
```
SELECT * 
FROM movies
WHERE name LIKE 'Se_en';
```
* LIKE is a special operator used with the WHERE clause to search for a specific pattern in a column.
* name LIKE 'Se_en' is a condition evaluating the name column for a specific pattern.
* Se_en represents a pattern with a wildcard character.
* The **_** means you can substitute any individual character here without breaking the pattern.
---
### %
% is another wildcard character that can be used with LIKE.
```
SELECT * 
FROM movies
WHERE name LIKE 'A%';
```
* % is a wildcard character that matches zero or more missing letters in the pattern. For example:
  * A% matches all movies with names that begin with letter ‘A’
  * %a matches all movies that end with ‘a’
* We can also use % both before and after a pattern:
  ```
  SELECT * 
  FROM movies 
  WHERE name LIKE '%man%';
  ``` 
  * Here any movie that contains the word ‘man’ in its name will be returned in the result.
  * LIKE is **not case sensitive**. ‘Batman’ and ‘Man of Steel’ will both appear in the result of the query above.

## IS NOT NULL
Unknown values are indicated by NULL.  
It is **not possible** to test for **NULL values** with **comparison operators**, such as = and !=.
```
SELECT name
FROM movies 
WHERE imdb_rating IS NOT NULL;
```

## BETWEEN
It's used in a WHERE **clause** to filter the result set within a certain **range**. It accepts **two values** that are either **numbers**, **text** or **dates**.
```
SELECT *
FROM movies
WHERE year BETWEEN 1990 AND 1999
```
The statement above filters the movies with years from 1990 uo to, and **including** 1999
* When the values are **text**, BETWEEN filters the result set for within the **alphabetical** range.
  ```
  SELECT *
  FROM movies
  WHERE name BETWEEN 'A' AND 'J';
  ```
  * Names that begin with the letter ‘A’ up to, but **not including** ones that begin with ‘J’. 
  * **However**, if a movie has a name of simply **‘J’**, it would actually **match**. 
  * Up to ‘J’, like ‘Jaws’, does not include.
* It is **case sensitive**

## AND 
Its  used to implement **multiple conditions**
```
SELECT * 
FROM movies
WHERE year BETWEEN 1990 AND 1999
   AND genre = 'romance';
```

## OR
Over the same logical of AND
```
SELECT *
FROM movies
WHERE year > 2014
   OR genre = 'action';
```
Using with WHEN
```
WHEN genre = 'romance' OR 'comedy' 
```
## ORDER BY
We can **sort** the results using ORDER BY, either **alphabetically** or **numerically**.
```
SELECT *
FROM movies
ORDER BY name;
```
Sometimes we want to sort things in a **decreasing** order. If we want to select all of the well-received movies by highest to lowest year:
```
SELECT *
FROM movies
WHERE imdb_rating > 8
ORDER BY year DESC;
```
- **DESC** is a keyword used in ORDER BY to sort the results in **descending** order (high to low or Z-A).
- **ASC** is a keyword used in ORDER BY to sort the results in **ascending** order (low to high or A-Z).

The column that we ORDER BY **doesn’t** even **have** to be one of the columns that we’re **displaying**.

Note: **ORDER BY** always goes **after WHERE** (if WHERE is present).

## LIMIT
Important to cap the number of rows in the result.  
It saves space on our screen and makes our queries run faster.
```
SELECT *
FROM movies
LIMIT 10;
```
LIMIT always goes at the very **end** of the query. Also, it is not supported in all SQL databases.  
Top 3 movies:
```
SELECT *
FROM movies
ORDER BY imdb_rating DESC
LIMIT 3;
```

## CASE
Used to create different outputs (usually in the SELECT statement).  
It is **SQL’s way** of handling **if-then logic**.  


Suppose we want to condense the ratings in movies to three levels:

- If the rating is above 8, then it is Fantastic.
- If the rating is above 6, then it is Poorly Received.
- Else, Avoid at All Costs.
```
SELECT name,
 CASE
  WHEN imdb_rating > 8 THEN 'Fantastic'
  WHEN imdb_rating > 6 THEN 'Poorly Received'
  ELSE 'Avoid at All Costs'
 END
FROM movies;
```
- Each **WHEN** tests a **condition** and the following **THEN** gives us the **string** **if** the condition is **true**.
- The **ELSE** gives us the **string if all** the above conditions are **false**.
- The CASE statement **must end** with **END**.

**IMPORTANT**  To shorten it, we can rename the column to ‘Review’ using AS:
```
SELECT name,
 CASE
  WHEN imdb_rating > 8 THEN 'Fantastic'
  WHEN imdb_rating > 6 THEN 'Poorly Received'
  ELSE 'Avoid at All Costs'
 END AS 'Review'
FROM movies;
```
It **need** the **comma** after the column name

## REVIEW
- **SELECT** is the clause we use every time we want to **query** information from a database.
- **AS** **renames** a **column** or table.
- **DISTINCT** return **unique** values.
- **WHERE** is a popular command that lets you **filter** the results of the query based on conditions that you specify.
- **LIKE** and **BETWEEN** are special operators.
- **AND** and **OR** combines **multiple conditions**.
- **ORDER** BY **sorts** the result.
- **LIMIT** specifies the **maximum** number of **rows** that the query will return.
- **CASE** creates **different outputs**.