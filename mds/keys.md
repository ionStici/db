# Database Keys

## Table of Contents

- [Introduction](#introduction)
  - [Importance of Database Keys](#importance-of-database-keys)
  - [Types of Database Keys](#types-of-database-keys)
- [Primary Key](#primary-key)
- [Key Validation](#key-validation)
- [Composite Primary Key](#composite-primary-key)
- [Foreign Key](#foreign-key)
  - [Placement of Foreign Keys](#placement-of-foreign-keys)
  - [Foreign Keys Query Example](#foreign-keys-query-example)

## Introduction

A **database key** is a specific column or a combination of columns within a table that is used to uniquely identify each row. Keys play a crucial role in ensuring data integrity and enforcing relationships between tables.

### Importance of Database Keys

- **Uniqueness:** Keys help avoid duplicate entries, ensuring that each record can be uniquely identified.
- **Data Integrity:** By placing constraints on key columns, database designers maintain the accuracy and consistency of the data within tables.
- **Relationships:** Keys facilitate the establishment of relationships between tables, enhancing the organization of data.

### Types of Database Keys

- **Primary Key:** A unique identifier for each row in a table, ensuring that no two rows can have the same value in this column.
- **Foreign Key:** A column or set of columns in one table that references the primary key in another table, establishing a relationship between the two.
- **Composite Key:** A key that consists of two or more columns to uniquely identify a row when a single column is insufficient.

## Primary Key

A **primary key** is a unique identifier for each row in a database table. The primary key ensures that each entry in the table is unique and cannot be `NULL`.

```sql
CREATE TABLE students (
  student_id INTEGER PRIMARY KEY,
  first_name VARCHAR(50),
  last_name VARCHAR(50)
)
```

In this example, the `student_id` uniquely identifies each student, ensuring that no two students have the same ID.

## Key Validation

To ensure that the keys designated for specific columns in a table are correctly set up, you can use the **information schema**. This schema provides metadata about the database, including details on tables, columns, and constraints.

The **information schema** is part of the SQL standard and offers read-only access to metadata. It allows you to query various aspects of your database structure.

To check if a column has been correctly designated as a primary key, you can query the `key_column_usage` view within the information schema. For example, to find the constraints on a `students` table:

```sql
SELECT
  constraint_name, table_name, column_name
FROM
  information_schema.key_column_usage
WHERE
  table_name = 'students';
```

This query will return a result set that shows the constraints applied to the `students` table:

```sql
 constraint_name | table_name | column_name
-----------------+------------+-------------
 students_pkey   | students   | student_id
```

- `constraint_name`: Indicates the name of the constraint, which typically follows a format like `table_name` + `_pkey` for primary keys.
- `table_name`: The name of the table.
- `column_name`: The column designated as the primary key.

This validation process helps ensure that your database design enforces uniqueness and integrity through proper key implementation.

## Composite Primary Key

A **composite primary key** is a key that consists of two or more columns in a table, used together to uniquely identify a row. This is necessary when no single column can serve as a unique identifier.

Consider a table named **enrollment** that tracks student enrollments in courses:

```sql
CREATE TABLE enrollment (
  student_id INTEGER,
  course_id INTEGER,
  enrollment_date DATE,
  PRIMARY KEY (student_id, course_id)  -- Composite Primary Key
);
```

- Each student can enroll in multiple courses, and each course can have multiple students.
- The combination of `student_id` and `course_id` ensures that each enrollment record is unique.

Using a composite primary key allows you to manage relationships effectively while preventing duplicate records that could arise from using single columns.

## Foreign Key

A **foreign key** is a column or a set of columns in one table that uniquely identifies a row in another table. It establishes a link between the two tables, ensuring data integrity.

Consider two tables: **users** and **orders**. Each order should be associated with a valid user:

```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100)
);

CREATE TABLE orders (
  order_id SERIAL PRIMARY KEY,
  order_date DATE,
  user_id INTEGER REFERENCES users(id)  -- Foreign Key
);
```

- The `user_id` column in the `orders` table is a foreign key that references the `id` column in the `users` table.
- This ensures that every order is associated with a valid user, preventing orphaned records in the `orders` table.

### Placement of Foreign Keys

When determining where to place a foreign key, consider the relationship:

- If a record in one table (e.g., `users`) must exist for a record in another table (e.g., `orders`) to be valid, the foreign key should be placed in the latter table.

### Foreign Keys Query Example

To retrieve a list of users and their associated orders, you would join the two tables:

```sql
SELECT users.name AS user_name, orders.order_date
FROM users
JOIN orders ON users.id = orders.user_id;
```

This query combines data from both tables based on the established relationship, providing a clear view of which users placed which orders.
