# A SQL SUMMARY
* A relational database is a database that organizes information into one or more tables. 

* Tables are sometimes referred to as relations.

* A statement is text that the database recognizes as a valid command. It always end in a semicolon ```;``` .

Exemple:
```
CREATE TABLE table_name (
   column_1 data_type, 
   column_2 data_type, 
   column_3 data_type
);
```
1. CREATE TABLE is a clause. Clauses perform specific tasks in SQL. By convention, clauses are written in capital letters. Clauses can also be referred to as commands.
2. table_name refers to the name of the table that the command is applied to.
3. (column_1 data_type, column_2 data_type, column_3 data_type) is a parameter. A parameter is a list of columns, data types, or values that are passed to a clause as an argument. Here, the parameter is a list of column names and the associated data type.

```
SELECT * FROM celebs;
```
1. SELECT and FROM are the clauses here.
2. We are applying the command to the celebs table.

## INSERT
The **INSERT** statement inserts a new row into a table.

```
INSERT INTO celebs (id, name, age) 
VALUES (1, 'Justin Bieber', 22);
```
* celebs is the **table** the row is added to.
* (id, name, age) is a **parameter** identifying the columns that data will be inserted into.
* VALUES is a **clause** that indicates the data being inserted.
* (1, 'Justin Bieber', 22) is a **parameter** identifying the values being inserted.
  * 1: an integer that will be added to id column
  * 'Justin Bieber': text that will be added to name column
  * 22: an integer that will be added to age column

## SELECT
**SELECT** statements are used to **fetch** data from a database.
```
SELECT name FROM celebs;
```
In the statement above, SELECT returns all data in the name column of the celebs table.
1. SELECT is a clause that indicates that the statement is a query. You will use SELECT every time you query data from a database.
2. name specifies the column to query data from.
3. FROM celebs specifies the name of the table to query data from. In this statement, data is queried from the celebs table.

```
SELECT * FROM celebs;
```
* ```*``` is a special wildcard character that allows you to select every column in a table

## ALTER
**ALTER TABLE** statement **adds** a **new** column to a table.

```
ALTER TABLE celebs 
ADD COLUMN twitter_handle TEXT;
```
1. ALTER TABLE is a clause that lets you make the specified changes.
2. celebs is the name of the table that is being changed.
3. ADD COLUMN is a clause that lets you add a new column to a table:
   * twitter_handle is the name of the new column being added
   * TEXT is the data type for the new column
4. NULL is a special value in SQL that represents missing or unknown data. Here, the rows that existed before the column was added have NULL (∅) values for twitter_handle.

## UPDATE
The **UPDATE** statement edits a **row** in a table.

```
UPDATE celebs
SET twitter_handle = '@taylorswift13'
WHERE id = 4;
```
1. UPDATE is a **clause** that edits a **row** in the table.
2. celebs is the name of the table.
3. SET is a **clause** that indicates the **column** to edit.

   * twitter_handle is the name of the column that is going to be updated
   * @taylorswift13 is the new value that is going to be inserted into the twitter_handle column.
4. WHERE is a **clause** that indicates which **row(s)** to update with the new column value. Here the row with a 4 in the id column is the row that will have the twitter_handle updated to @taylorswift13.

## DELETE 
The **DELETE FROM** statement deletes one or more rows from a table.
```
DELETE FROM celebs
WHERE twitter_handle IS NULL;
```
1. **DELETE FROM** is a **clause** that lets you delete **rows** from a table.
2. celebs is the name of the table we want to delete rows from.
3. **WHERE** is a **clause** that lets you select **which rows** you want to delete. Here we want to delete all of the rows where the twitter_handle column IS NULL.
4. **IS NULL** is a **condition** in SQL that returns true when the value is NULL and false otherwise.

## Constraints
**Constraints** add information about **how** a **column** can be used. 
* They are invoked after specifying the data type for a column.
* They can be used to tell the database to reject inserted data that does not adhere to a certain restriction.
```
CREATE TABLE celebs (
   id INTEGER PRIMARY KEY, 
   name TEXT UNIQUE,
   date_of_birth TEXT NOT NULL,
   date_of_death TEXT DEFAUT 'Not Applicable'
);
```
1. **PRIMARY KEY** columns can be used to uniquely **identify** the **row**. Attempts to insert a row with an identical value to a row already in the table will result in a constraint violation which will not allow you to insert the new row.

2. **UNIQUE** columns have a different value for every row. This is **similar** to **PRIMARY KEY** **except** a table **can** have **many different UNIQUE columns**.

3. **NOT NULL** columns **must have a value**. Attempts to insert a row without a value for a NOT NULL column will result in a constraint violation and the new row will not be inserted.

4. **DEFAULT** columns take an **additional argument** that will be the assumed value for an inserted row **if** the new **row** does **not specify** a **value** for that **column**.

## REVIEW
* **CREATE TABLE** creates a new table.
* **INSERT INTO** adds a new row to a table.
* **SELECT** queries data from a table.
* **ALTER TABLE** changes an existing table.
* **UPDATE** edits a row in a table.
* **DELETE FROM** deletes rows from a table.