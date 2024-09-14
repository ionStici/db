# SQL (Structure Query Language)

## Table of Content

- [Introduction](#introduction)
- [SQL Statements](#sql-statements)
  - [Example of Creating a Table](#example-of-creating-a-table)
  - [Components of a SQL command](#components-of-a-sql-command)
  - [Example of a `SELECT` statement](#example-of-a-select-statement)
- [SQL Operations](#sql-operations)
  - [1. Create](#1-create)
  - [2. Insert](#2-insert)
  - [3. Select](#3-select)
  - [4. Alter](#4-alter)
  - [5. Update](#5-update)
  - [6. Delete](#6-delete)
- [SQL Constraints](#sql-constraints)
- [Review of Key SQL Operations](#review-of-key-sql-operations)

## Introduction

**SQL (Structure Query Language)** is a programming language designed to manage data stored in relational databases. SQL operates through simple, declarative statements to **query**, **insert**, **update**, and **delete** data.

- **Relational Database** : Organizes information into **tables** (relations).

- **Table** : A collection of data organized into **rows** (records) and **columns** (fields).

- **Columns** : A vertical set of data values of a specific data type (e.g `INTEGER`, `TEXT`).

- **Row** : A single record in the table, containing one value for each column.

Each table stores data with defined **data types**, such as:

- `INTEGER` for whole numbers,
- `TEXT` for strings,
- `REAL` for decimal values (floating-point numbers),
- `DATE` for dates (`YYYY-MM-DD`).

## SQL Statements

A **statement** is a command recognized by the database, ending with a semicolon `;`

### Example of Creating a Table

```sql
CREATE TABLE table_name (
  column_1 data_type,
  column_2 data_type,
  column_3 data_type
);
```

### Components of a SQL command

1. **Clauses** : Keywords that perform specific actions. For example, `CREATE TABLE` is a clause that tells the database to create a table. By convention, clauses are written in uppercase.

2. **Table Name** : `table_name` refers to the name of the table that the command is applied to.

3. **Parameters** : `(column_1 data_type, ...)` parameter defines columns and their data types. A parameter is a list of column names, data types, values, conditions, that are passed to a clause as an argument.

### Example of a `SELECT` statement

```sql
SELECT * FROM users;
```

- `SELECT` : clause to fetch data.
- `*` : Wildcard to select all columns.
- `FROM users` : Specifies the table (`users`) from which to retrieve data.

## SQL Operations

### 1. Create

The `CREATE` statement is used to create new tables in the database.

```sql
CREATE TABLE friends (
  id INTEGER,
  name TEXT,
  age INTEGER
)
```

1. `CREATE TABLE` : Creates a bew table named `friends`.

2. `(id INTEGER, name TEXT, age INTEGER)` is a list of parameters defining each column in the table and its data type.

### 2. Insert

The `INSERT` statements adds new rows (records) to a table.

```sql
INSERT INTO friends (id, name, age)
VALUES (1, 'Irene', 25);
```

1. `INSERT INTO` : Is a clause that inserts a new row into the specified table (`friends`).
2. `(id, name, age)` : is a parameter identifying the columns that the data will be inserted into.
3. `VALUES` : Clause that specifies the values to insert for each column.
4. `(1, 'John', 26);` is a parameter identifying the values being inserted.

### 3. Select

The `SELECT` statement retrieves data from one or more columns in a table.

```sql
SELECT name FROM friends;
```

1. `SELECT` : Clause that specifies what data to retrieve (query `name` columns)
2. `FROM users` : specifies the name of the table to query data from.

Use `*` to query all columns from a table:

```sql
SELECT * FROM friends;
```

`SELECT` statements always return a new table called the **result set**.

### 4. Alter

The `ALTER TABLE` statement modifies an existing table by adding or removing columns, or altering their properties.

```sql
ALTER TABLE friends
ADD COLUMN facebook TEXT;
```

1. `ALTER TABLE` : is a clause that lets you make changes to the specified table (`friends`).
2. `ADD COLUMN facebook TEXT` adds the `facebook` column of type `TEXT` to the table.
3. Pre-existing rows will have `NULL` in the new column. `NULL` represents a missing or unknown data.

### 5. Update

The `UPDATE` statement modifies existing records in a table.

```sql
UPDATE friends
SET facebook = 'fb.com'
WHERE id = 1;
```

1. `UPDATE` : Edits a record in the `friends` table.
2. `SET` : clause that specifies the column to edit (`facebook`) and the new value (`fb.com`).
3. `WHERE` : is a clause that indicates the condition for which the row(s) are updated with the new column data.

### 6. Delete

The `DELETE` statement deletes rows from a table.

```sql
DELETE FROM friends
WHERE facebook IS NULL;
```

1. `DELETE FROM` : Deletes rows from the `friends` table.
2. `WHERE` : Is a clause that lets you select which rows to delete based on a condition.
3. `facebook IS NULL` : is a condition in SQL that returns true when the value is `NULL` and false otherwise.
   (rows with `NULL` in the `facebook` column).

## SQL Constraints

Constraints enforce rules for columns and ensure data integrity. Constraints can be used to tell the database to reject inserted data that does not adhere to a certain restriction.

```sql
CREATE TABLE friends (
  id INTEGER PRIMARY KEY,
  username TEXT UNIQUE,
  name TEXT DEFAULT '',
  age INTEGER NOT NULL
);
```

1. `PRIMARY KEY` : Ensures each value in the `id` column is unique and can uniquely identify a row.

2. `UNIQUE` : Ensures the `username` column contains unique values for each row.

3. `DEFAULT` : Provides a default value (`''`) for `name` column if not explicitly provided.

4. `NOT NULL` : Ensures `age` column cannot have `NULL` values.

## Review of Key SQL Operations

SQL is a programming language designed to manipulate and manage data stored in relational databases.

- A relational database is a database that organizes information into one or more tables.
- A table is a collection of data organized into rows and columns.

A statement is a string of characters that the database recognizes as a valid command.

- `CREATE TABLE` : Creates a new table.
- `INSERT INTO` : Adds new rows to a table.
- `SELECT` : Queries data from a table.
- `ALTER TABLE` : Modifies the structure of a table.
- `UPDATE` : Changes data in existing rows.
- `DELETE FROM` : Deletes rows from a table.
- **Constraints** : Add rules (e.g. `PRIMARY KEY`, `UNIQUE`, `DEFAULT`, `NOT NULL`) to ensure data integrity.
