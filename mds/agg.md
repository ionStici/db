# Aggregate Functions

## Table of Contents

- [Introduction](#introduction)
- [Count](#count)
- [Sum](#sum)
- [Max / Min](#max--min)
- [Average](#average)
- [Round](#round)
- [Group By](#group-by)
  - [Column Reference](#column-reference)
  - [Important Notes](#important-notes)
  - [Filter Groups with Having](#filter-groups-with-having)
  - [Group By Example](#group-by-example)

## Introduction

**Aggregates** : calculations performed on multiple rows of a table.

- `COUNT()` : count the number of row.
- `SUM()` : the sum of the values in a column.
- `MAX()` / `MIN()` : the largest/smallest value.
- `AVG()` : the average of the values in a column.
- `ROUND()` : round the values in the column.

## Count

Calculate how many rows are in a table.

```sql
SELECT COUNT(*) -- Every row
FROM table_name;
```

`COUNT()` is a function that takes the name of a column as an argument and counts the number of non-empty values in that column.

## Sum

The `SUM()` function takes the name of a column as an argument and returns the sum of all the values in that column.

```sql
SELECT SUM(downloads)
FROM apps;
```

## Max / Min

The `MAX()` and `MIN()` functions take the name of a column as an argument and return the highest and lowest value in that column.

```sql
SELECT MAX(downloads) FROM apps;
```

## Average

`AVG()` calculates the average value of a particular column.

```sql
SELECT AVG(downloads) FROM apps;
```

## Round

`ROUND()` takes 2 arguments: (1) a column name, (2) an integer representing the number of decimals.

```sql
SELECT ROUND(price, 0) FROM fake_apps;
```

## Group By

The `GROUP BY` clause in SQL is used to organize identical data into groups and is typically used in conjunction with aggregate functions. If allows you to perform operations on each group of data rather than on the entire dataset.

```sql
SELECT year, AVG(rating) AS average_rating FROM movies
GROUP BY year
ORDER BY year;
```

- The `movies` table is grouped by the `year` column.
- For each year, the average rating is calculated.
- The result is sorted by year.

### Column Reference

You can use column positions in the `GROUP BY` clause:

```sql
SELECT ROUND(rating), COUNT(name) FROM movies
GROUP BY 1
ORDER BY 1;
```

Here, `1` refers to the first column in the `SELECT` list, which is `ROUND(rating)`. This query groups the data by the rounded rating values and counts the number of names in each group.

### Important Notes

- The `GROUP BY` clause must come after any `WHERE` clause but before the `ORDER BY` and `LIMIT` clauses in your SQL statement.
- Every column in the `SELECT` clause that is not an aggregate function must be included in the `GROUP BY` clause.

### Filter Groups with Having

Filter groups with `HAVING`: which groups to include and which to exclude.

All types of `WHERE` clauses can be used with `HAVING`, but for groups.

```sql
SELECT year, genre, COUNT(name) FROM movies
GROUP BY 1, 2
HAVING COUNT(name) > 10;
```

`HAVING` statement always comes after `GROUP BY`, but before `ORDER BY` and `LIMIT`.

- `WHERE` : filter results of a query based on values of individual rows.
- `HAVING` : filter results of a query based on an aggregate property.

### Group By Example

```sql
-- Calculate the average price of apartments in each neighborhood
SELECT neighborhood, AVG(price)
FROM apartments
GROUP BY neighborhood;
```
