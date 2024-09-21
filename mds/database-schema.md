# Designing a Database Schema

## Table of Contents

- [What is a Database Schema](#what-is-a-database-schema)
  - [Creating a Database Schema](#creating-a-database-schema)
- [Creating Tables](#creating-tables)
- [Querying Tables](#querying-tables)
  - [Inserting Data](#inserting-data)
  - [Querying Data](#querying-data)
- [Relationships Between Tables](#relationships-between-tables)
  - [Types of Relationships](#types-of-relationships)
  - [Implementing Relationships](#implementing-relationships)
  - [Querying Related Data](#querying-related-data)
- [**Data Types in PostgreSQL**](#data-types-in-postgresql)

## What is a Database Schema

A **database schema** defines the structure of a database, including how data is organized into tables and how tables relate to one another.

### Creating a Database Schema

When designing a database schema, consider the following steps:

1. Define the purpose of the database.
2. Identify the necessary information.
3. Organize the information into tables.
4. Structure tables with appropriate columns.
5. Minimize redundancy to ensure accuracy and efficiency.
6. Identify relationships between tables.

These steps help maintain data integrity and make querying efficient.

## Creating Tables

When designing a schema, evaluate whether to consolidate information into a single table or split it into multiple tables. Once tables are identified, define their structure. A table consists of columns with specific names and data types.

```sql
CREATE TABLE table_name (
  column_name data_type,
  ...
);
```

```sql
CREATE TABLE products (
  title varchar(25),
  qty integer
)
```

PostgreSQL naming convention: snake case.

## Querying Tables

### Inserting Data

To populate a PostgreSQL table with data, you use the `INSERT INTO` statement. This command allows you to add new rows to your table.

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

```sql
INSERT INTO products (title, qty, price)
VALUES ('Laptop', 5, 1200);
```

### Querying Data

To retrieve data from a table, you use the `SELECT` statement. This allows you to specify which columns to return.

```sql
SELECT column1, column2, ...
FROM table_name;
```

```sql
SELECT title, qty
FROM products;
```

## Relationships Between Tables

In a relational database, tables can be connected through relationships. These relationships help organize data and allow for more complex queries.

### Types of Relationships

- **One-to-One:** Each row in one table corresponds to exactly one row in another table.
- **One-to-Many:** A single row in one table can relate to multiple rows in another table. This is the most common relationship.
- **Many-to-Many:** Rows in one table can relate to multiple rows in another table and vice versa, often managed through a junction table.

Example of a One-to-Many Relationship: Consider two tables, **products** and **orders**, where each order references specific products from the **products** table.

### Implementing Relationships

To establish a relationship, you typically use a **foreign key**. A foreign key in one table points to a primary key in another table, creating a link between the two.

```sql
CREATE TABLE authors (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100)
);

CREATE TABLE books (
  id SERIAL PRIMARY KEY,
  title VARCHAR(100),
  author_id INTEGER REFERENCES authors(id)
);
```

### Querying Related Data

To retrieve related data from multiple tables, you can use joins. A join allows you to combine rows from different tables based on a related column.

```sql
SELECT authors.name, books.title
FROM authors
JOIN books ON authors.id = books.author_id;
```

This query returns a list of authors along with the titles of the books they have written.

## Data Types in PostgreSQL

1. **`integer`**

   - **Description:** Whole number without a fractional component.
   - **Example:** `712`, `-42`, `0`
   - **Usage:** Ideal for counting, indexing, and any situation requiring whole numbers.

2. **`decimal`**

   - **Description:** Floating-point number with a specified precision and scale.
   - **Example:** `26.17345`, `-100.99`
   - **Usage:** Used when exact precision is required, such as financial calculations. You can define it as `decimal(10, 5)`, which means up to 10 digits, with 5 after the decimal point.

3. **`money`**

   - **Description:** A fixed-point number specifically designed to represent currency values, formatted with two decimal places.
   - **Example:** `6.17`, `-100.00`
   - **Usage:** Useful for financial applications where currency representation is needed.

4. **`boolean`**

   - **Description:** A data type representing logical values: either `TRUE` or `FALSE`.
   - **Example:** `TRUE`, `FALSE`
   - **Usage:** Commonly used for flags or binary conditions (e.g. is_active, is_verified).

5. **`char(n)`**

   - **Description:** A fixed-length string type. If the input string is shorter than `n`, it is padded with spaces.
   - **Example:** `char(3)` storing `'12 '` will result in `'12 '` (with one space).
   - **Usage:** Useful when the length of the string is known and constant, such as postal codes.

6. **`varchar(n)`**

   - **Description:** A variable-length string type that can hold up to `n` characters.
   - **Example:** `varchar(20)` can store any string up to `20` characters long.
   - **Usage:** Ideal for user input where the length can vary, such as names or email addresses.

7. **`text`**

   - **Description:** An unlimited-length string type that can store strings of any size.
   - **Example:** `'Hello World'`
   - **Usage:** Useful for large bodies of text, like descriptions, comments, or articles.

8. **`bigint`**

   - **Description:** A larger integer type that can store values from -2^63 to 2^63-1.
   - **Example:** `9223372036854775807`
   - **Usage:** Used when very large integers are needed, such as population counts or large sums.

9. **`smallint`**

   - **Description:** A smaller integer type that can store values from -32,768 to 32,767.
   - **Example:** `123`
   - **Usage:** Useful for saving space when you know the numbers will be within this range.

10. **`bytea`**

    - **Description:** A data type for storing binary data (byte arrays).
    - **Example:** `'\xDEADBEEF'` (hexadecimal representation of binary data).
    - **Usage:** Useful for storing images, files, or other binary data.

11. **`json`**

    - **Description:** A data type for storing JSON (JavaScript Object Notation) data.
    - **Example:** `'{"name": "John", "age": 30}'`
    - **Usage:** Useful for storing semi-structured data, allowing for flexible data formats.

12. **`jsonb`**

    - **Description:** A binary format for storing JSON data, allowing for more efficient processing and indexing.
    - **Example:** `'{ "name": "John", "age": 30 }'`
    - **Usage:** Preferred over `json` for performance and functionality when working with JSON data.

13. **`date`**

    - **Description:** Stores calendar dates (year, month, day).
    - **Example:** `'2023-09-15'`
    - **Usage:** Useful for storing dates in applications, such as birthdays or event dates.

14. **`timestamp`**

    - **Description:** Stores both date and time values.
    - **Example:** `'2023-09-15 14:30:00'`
    - **Usage:** Ideal for logging events that occur at specific times.

15. **`interval`**

    - **Description:** Represents a time span or duration.
    - **Example:** `'2 days 3 hours'`
    - **Usage:** Useful for calculating time differences or durations.
