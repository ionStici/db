# Multiple Tables

## Table of Contents

- [Introduction](#introduction)
- [Combining Tables with SQL](#combining-tables-with-sql)
- [Left Joins](#left-joins)
- [Primary Key vs Foreign Key](#primary-key-vs-foreign-key)
- [Cross Join](#cross-join)
- [Union](#union)
- [With](#with)

## Introduction

**SQL Joins** : combine rows from two or more tables based on a related column between them.

## Combining Tables with SQL

The `JOIN` clause combines rows from two or more tables by joining them together with other results based on common column values specified using an `ON` condition.

```sql
SELECT orders.title, customers.name
FROM orders
JOIN customers
  ON orders.id = customers.id;
```

When we perform an inner join, the result only includes rows that match the `ON` condition.

## Left Joins

A left join will keep all rows from the first table, regardless of whether there is a matching row in the second table.

```sql
SELECT *
FROM table1
LEFT JOIN table2
ON table1.id = table2.id;
```

1. The first line select all columns from both tables.
2. The second line select `table1` (the "left" table).
3. The third line performs a `LEFT JOIN` on `table2` (the "right" table).
4. The fourth line tells SQL how to perform the join (by looking for matching values in column `id`).

## Primary Key vs Foreign Key

**Primary keys** are special columns that are used to uniquely identify each row of a table in SQL.

**Primary Keys requirements:** (1) none of the values can be `NULL`, (2) each value must be unique, (3) a table can not have more than one primary key column.

When the primary key for one table appears in a different table, it is called a **foreign key**.

Generally, the primary key is called `id`, and foreign keys have more descriptive names such as `products_id`.

The most common types of joins will be joining a foreign key from one table with the primary key from another table.

```sql
SELECT * FROM products JOIN orders
ON products.id = orders.product_id;
```

## Cross Join

Combine rows:

```sql
SELECT table1.c1, table2.c2
FROM table1
CROSS JOIN table2;
```

It combines every row in one table with every row in another table (which actually is not very useful).

## Union

**Union:** Stack one dataset on top of the other.

```sql
SELECT *
FROM table1
UNION
SELECT *
FROM table2;
```

Rules: (1) table must have the same number of columns, (2) the columns must have the same data types in the same order as the first table.

## With

The `WITH` statement allows us to perform a separate query.

```sql
WITH previous_query AS (
  SELECT * FROM table1
)
SELECT previous_query.name, table2.description
FROM previous_query
JOIN table2
ON previous_query.id = table2.id;
```

Essentially, we can put a whole query inside the parentheses `()` of the `WITH` clause and give it a name.

After that, we can use this name as if it's a table and write a new query using the first query.
