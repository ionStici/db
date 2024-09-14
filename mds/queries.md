# Querying with `SELECT`

## Table of Contents

- [Select Columns](#select-columns)
- [Using Aliases](#using-aliases)
- [Remove Duplicate Values](#remove-duplicate-values)
- [Filtering Results with `WHERE`](#filtering-results-with-where)
  - [Comparison Operators with `WHERE`](#comparison-operators-with-where)
- [`LIKE` for Pattern Matching](#like-for-pattern-matching)
- [Null](#null)
- [Between](#between)
- [AND](#and)
- [OR](#or)
- [Order By](#order-by)
  - [Order the movie's title from A to Z](#order-the-movies-title-from-a-to-z)
  - [Order Numeric Values](#order-numeric-values)
- [Limit](#limit)
- [Case](#case)

## Select Columns

The `SELECT` statement is used to query data from a database.

```sql
-- Query all columns
SELECT * FROM movies;

-- Query specific columns
SELECT column_1, column_2, column_3
FROM movies;
```

## Using Aliases

The `AS` keyword is used to give the column a temporary new name in the query result. The original column name in the table remains unchanged. Useful for making query results more readable.

```sql
-- Rename the result column 'name' as 'title'
SELECT name AS title
FROM movies;
```

## Remove Duplicate Values

Use `DISTINCT` to remove duplicate values from the result set.

```sql
-- Select only the distinct values
SELECT DISTINCT tools FROM inventory;
```

`DISTINCT` ensures that only unique values are returned. If multiple rows contain the same value in the column, they will only appear once in the result set.

## Filtering Results with `WHERE`

The `WHERE` clause allows you to filter records by specifying a condition.

```sql
-- Query movies with a rating greater than 8
SELECT *
FROM movies
WHERE rating > 8;
```

### Comparison Operators with `WHERE`

Operators used in combination with the `WHERE` clause to compare column values:

| Operators                     |
| ----------------------------- |
| `=` equal to                  |
| `!=` not equal to             |
| `>` greater than              |
| `<` less than                 |
| `>=` greater than or equal to |
| `<=` less than or equal to    |

## `LIKE` for Pattern Matching

`LIKE` is an operator used with the `WHERE` clause to search for a specific pattern in a column (not case sensitive).

```sql
SELECT *
FROM movies
WHERE name LIKE 'hello %';
```

The `%` wildcard represents any sequence of characters.

- `LIKE 'hello %'` : matches any movie that starts with `'hello'`
- `LIKE %spider%` : matches any movie that has the string `'spider'` in its `name`.

The `_` wildcard character means you can substitute any individual character.

- `WHERE name LIKE 'Se_en';` : `Seven` or `Se7en` both match.

## Null

`IS NULL` and `IS NOT NULL` for identifying rows with missing values.

```sql
SELECT name FROM movies
WHERE rating IS NOT NULL;
```

## Between

Filter results within a certain range.

```sql
SELECT * FROM movies
WHERE year BETWEEN 2000 AND 2010;
-- WHERE name BETWEEN 'A' AND 'J';
```

`BETWEEN` accepts 2 values that are either **numbers, text, or dates**.

## AND

Combine multiple conditions in a `WHERE` clause.

```sql
SELECT * FROM movies
WHERE year BETWEEN 1990 and 1999 AND genre = 'romance';
```

With `AND`, both conditions must be true for the row to be included in the result.

## OR

`OR` operator can be used to combine multiple conditions in `WHERE`. If any condition is true, it will return the row.

```sql
SELECT * FROM movies
WHERE genre = 'romance' OR genre = 'comedy';
```

## Order By

Use `ORDER BY` clause to sort the result set in either **ascending** (`ASC` default), or **descending** (`DESC`) order, either alphabetically or numerically.

Note: if `WHERE` is present, then `ORDER BY` always goes after.

### Order the movie's title from A to Z

```sql
SELECT * FROM movies
ORDER BY name;
```

### Order Numeric Values

```sql
SELECT * FROM movies
ORDER BY year DESC;
```

- `DESC` : keyword used in `ORDER BY` to sort the results in descending order (high to low or Z-A).
- `ASC` : sort the results in ascending order (low to high or A-Z).

## Limit

Use the `LIMIT` clause to restrict the number of rows returned by a query.

```sql
SELECT * FROM movies
LIMIT 10;
```

## Case

A `CASE` statement allows us to create different outputs. It is SQL's way of handling if-then logic.

```sql
SELECT name,
  CASE
    WHEN rating > 8 THEN 'Good'
    WHEN rating > 6 THEN 'Meh'
    ELSE 'Bad'
  END AS 'Review'
FROM movies;
```

- Each `WHEN` tests a condition and the following `THEN` gives a string if the condition is true.
- The `ELSE` gives a string if all the above conditions are false.
- The `CASE` statement must end with `END`.
