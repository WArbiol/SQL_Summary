# MULTIPLE TABLES
Join related information across multiple tables.  
We’ll learn the SQL commands that will help us work with data that is stored in multiple tables.  

We're goint to work with three tables:
- orders
- subscriptions
- customers
### **orders**
(a table with information on each magazine purchase)
|order_id|customer_id|subscription_id|purchase date|
|--- |--- |--- |---          |
|1   |  2 |   3| 2017-01-01  |
| 2  |  2 |   2| 2017-01-01  |
| 3  |  3 |   1| 2017-01-01  |

### **subscriptions**
(a table that describes each type of subscription)
|subscription_id|description|price_per_month|length|
|---|---|---|---|
|1   |Politics Magazine |   5| 12 months  |
| 2  |  Fashion Magazine |   10| 6 months  |
| 3  |  Sports Magazine |   7| 3 months  |

### **customers**
(a table with customer names and contact information)
|customer_id|customer_name|address|
|---|---|---|
| 1  |  John Smith |   123 Main St|
| 2  |  Jane Doe |   456 Park Ave|
| 3  |  Joe Schmo |   798 Broadway|

The description of the magazine ordered in **order_id 1** is the **Sports Magazine**, because by the first table we can notice that the **subscription_id is 3**

## JOIN
It's used to **combining tables**.

If we want to combine **orders** and **customers**, we would type:

```
SELECT *
FROM orders
JOIN customers
  ON orders.customer_id = customers.customer_id;
```
1. The **first line** selects **all columns from our combined table**. If we only want to select certain columns, we can specify which ones we want.
2. The **second line** specifies **the first table** that we want to **look in**, orders
3. The **third line** uses **JOIN** to say that we want to **combine information** from orders with customers.
4. The **fourth line** tells us **how to combine** the two tables. We want to match orders table’s customer_id column with customers table’s customer_id column.

The syntax **table_name.column_name** to be sure that our requests for columns are **unambiguous**.  
We will also use it in the SELECT or any other statement.

If we only wanted to select orders table’s order_id column and customers table’s customer_name column, we could use the following query:
```
SELECT orders.order_id,
   customers.customer_name
FROM orders
JOIN customers
  ON orders.customer_id = customers.customer_id;
```
Now there is no ambiguity.

Another example:
```
SELECT *
FROM orders
JOIN subscriptions
  ON orders.subscription_id = subscriptions.subscription_id
WHERE description = 'Fashion Magazine';
```

## Inner Join
When we perform a simple JOIN (often called an inner join) our result only includes rows that match our ON condition.

### **Table 1**
|C1 |C2     |          
|---|---    |          
| A | **B** |          
| Q | W     |          
| X | **Y** |          
### **Table 2**
|C2     |C3 |
|---    |---|
| **B** | C |
| E     | R |
| **Y** | Z |

### **INNER JOIN**
|C1  |C2     |C3 |
|--- |---    |---|
| A  | **B** | C |
| X  | **Y** | Z |

## LEFT JOIN
It's used to **combine** two tables and **keep** some of the **un-matched rows**.

A left join will keep all rows from the first table, regardless of whether there is a matching row in the second table.

### **LEFT JOIN** Table 1 + Table 2
|C1 |C2     | C3          
|---|---    |---        
| A | **B** | C         
| Q | W     |          
| X | **Y** | Z  

The final result will **keep all rows** of the **first table** but will **omit** the **un-matched row** from the **second table**.

The left join above represents a table operation produced by the following command:

```
SELECT *
FROM table1
LEFT JOIN table2
  ON table1.c2 = table2.c2;
```
To find out how many people is subscribed on Newspaper but not on online articles:
```
SELECT COUNT(*)
FROM newspaper
LEFT JOIN online
  ON newspaper.ID = online.ID
WHERE online.id IS NULL;
```
## Primary Key vs Foreign Key
Let’s return to our example of the magazine subscriptions.  We have three tables: **orders**, **subscriptions**, and **customers**.

Each of these tables has a column that uniquely identifies each row of that table:

- order_id for orders
- subscription_id for subscriptions
- customer_id for customers

These special columns are called **primary keys**.

Primary keys have a few requirements:

- None of the values can be NULL.
- Each value must be unique (i.e., you can’t have two customers with the same customer_id in the customers table).
- A table can not have more than one primary key column.

Reexamining the orders table:

|order_id|customer_id|subscription_id|purchase date|
|--- |--- |--- |---          |
|1   |  2 |   3| 2017-01-01  |
| 2  |  2 |   2| 2017-01-01  |
| 3  |  3 |   1| 2017-01-01  |

Both customer_id (the primary key for customers) and subscription_id (the primary key for subscriptions) appear in this. These are **foreign key**.

When the primary key for one table appears in a different table, it is called a **foreign key**.

So **customer_id** is a **primary key when** it appears in **customers**, but a **foreign key when** it appears in **orders**.

**Generally**, the **primary key** will just be **called id**. **Foreign** keys will have **more descriptive** names.

*Why is this important?* The most common types of joins will be joining a foreign key from one table with the primary key from another table. 

Example:
```
SELECT *
FROM classes
JOIN students
on classes.id = students.class_id
```

## CROSS JOIN
So far, we’ve focused on matching rows that have some information in common.  
**Cross join** serves to just **combine all rows** of one table with all rows of another table.

For instance, if we had a table of shirts and a table of pants, we might want to know **all the possible combinations** to create different outfits:
```
SELECT shirts.shirt_color,
   pants.pants_color
FROM shirts
CROSS JOIN pants; 
```
- The first two lines select the columns shirt_color and pants_color.
- The third line pulls data from the table shirts.
- The fourth line performs a CROSS JOIN with pants.

Notice that cross joins **don’t require** an **ON** statement. You’re not really **joining** on **any columns**!

If we have **3 different shirts** (white, grey, and olive) and **2 different pants** (light denim and black), the results might look like this:

| shirt_color | pants_color |
|-------------|-------------|
| white       | light denim |
| white       | black       |
| grey        | light denim |
| grey        | black       |
| olive       | light denim |
| olive       | black       |

A more **common usage** of **CROSS JOIN** is when we need to **compare** each **row** of a table **to a list of values**.

The newspaper's table has to columns that we haven't discussed: **start_month** and 
**end_month**.  
Suppose we wanted to know how many **users** were **subscribed during each month** of the year using **cross join**. 

Number of costumers on March:
```
SELECT COUNT(*)
FROM newspaper
WHERE start_month <= 3 AND end_month >= 3;
```
With all months we have the taable monsths to help us:
| month |
|:-----:| 
|   1   | 
|   2   |
|   3   |
|   4   |
|   5   |
|   6   |
|   7   |
|   8   |
|   9   |
|   10  |
|   11  |
|   12  |

The code:
```
SELECT *
FROM newspaper
CROSS JOIN months;
```
Will return each row of newspaper 12 times for each month.

This one:
```
SELECT *
FROM newspaper
CROSS JOIN months
WHERE start_month <= month and end_month >= month;
```
Will return each row of newspaper n times. if the subscriber stayed 5 months, n=5, example:
| first_name | start_month | end_month | month | end_month | month |
|:----------:|:-----------:|:---------:|:-----:|:---------:|:-----:|
|   Vinnie   |      1      |     5     |   1   |     5     |   1   |
|   Vinnie   |      1      |     5     |   2   |     5     |   2   |
|   Vinnie   |      1      |     5     |   3   |     5     |   3   |
|   Vinnie   |      1      |     5     |   4   |     5     |   4   |
|   Vinnie   |      1      |     5     |   5   |     5     |   5   |
|  Francesco |      1      |     5     |   1   |     5     |   1   |
|  Francesco |      1      |     5     |   2   |     5     |   2   |
|  Francesco |      1      |     5     |   3   |     5     |   3   |
|  Francesco |      1      |     5     |   4   |     5     |   4   |
|  Francesco |      1      |     5     |   5   |     5     |   5   |

So now we just need to count by month:

```
SELECT month,
   COUNT(*) AS 'subscribers'
FROM newspaper
CROSS JOIN months
WHERE start_month <= month 
   AND end_month >= month
GROUP BY month;
```
And we get:
| month | subscribers |
|:-----:|:-----------:|
|   1   |      2      |
|   2   |      9      |
|   3   |      13     |
|   4   |      17     |
|   5   |      27     |
|   6   |      30     |
|   7   |      20     |
|   8   |      22     |
|   9   |      21     |
|   10  |      19     |
|   11  |      15     |
|   12  |      10     |

## UNION
Union of tables:  
### Table1:
| pokemon    | type  |
|------------|-------|
| Bulbasaur  | Grass |
| Charmander | Fire  |
| Squirtle   | Water |
### Table2:
| pokemon | type   |
|---------|--------|
| Snorlax | Normal |

```
SELECT *
FROM table1
UNION
SELECT *
FROM table2;
```
### Output:
| pokemon    | type   |
|------------|--------|
| Bulbasaur  | Grass  |
| Charmander | Fire   |
| Squirtle   | Water  |
| Snorlax    | Normal |

SQL has strict rules for appending data:

- Tables must have the same number of columns.
- The columns must have the same data types in the same order as the first table.

Attaching newspaper and online:

```
SELECT *
FROM newspaper
UNION
SELECT *
FROM online
```

## WITH
It's used to join the results of a query with a table.

For instance, the number of subscriptions for each subscriber:
```
SELECT customer_id, 
  COUNT(subscription_id) AS 'subscriptions'
FROM orders
GROUP BY customer_id;
```
| customer_id | subscriptions |
|:-----------:|:-------------:|
|      1      |       4       |
|      2      |       1       |
|      3      |       6       |
|      4      |       2       |

But it give with the customer_id, but we want **with the custumer's name**.

**Do not include ; inside of the ( ) of your WITH statement.**

To put the name we can do in this way:
```
WITH previous_query AS (
  SELECT customer_id, 
    COUNT(subscription_id) AS 'subscriptions'
  FROM orders
  GROUP BY customer_id
)
SELECT customers.customer_name, 
  previous_query.subscriptions
FROM previous_query
JOIN customers 
  ON previous_query.customer_id = customers.customer_id;
```

## REVIEW
- **JOIN** will **combine rows** from different tables **if** the join **condition** is true.

- **LEFT** JOIN will **return every row** in the left table, and if the join condition is not met, NULL values are used to fill in the columns from the right table.

- **Primary key** is **a column** that serves a unique **identifier** for **the rows** in the table.

- **Foreign key** is **a column** that **contains** the **primary** key to **another table**.

- **CROSS JOIN** lets us **combine all rows** of one table with all rows of another table.

- **UNION** stacks one dataset on top of another.

- **WITH** allows us to **define one or more temporary tables** that can **be used** in the final query.