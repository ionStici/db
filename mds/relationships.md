# Database Relationships

## Table of Contents

- [Introduction](#introduction)
- [One-to-One Relationship](#one-to-one-relationship)
- [One-to-Many Relationship](#one-to-many-relationship)
- [Many-to-Many Relationship](#many-to-many-relationship)

## Introduction

A **database relationship** establishes the way in which connected tables are dependent on one another. Three types of relationships: one-to-one, one-to-many and many-to-many.

## One-to-One Relationship

A **one-to-one relationship** exists when a row in one table is associated with exactly one row in another table, and vice versa. This relationship ensures that each record is uniquely paired.

Consider a **user** table and a **profile** table:

- **User Table**:
  - user_id (Primary Key)
  - username
  - email
- **Profile Table**:
  - profile_id (Primary Key)
  - user_id (Foreign Key)
  - bio

Each user has one profile, and each profile belongs to one user. The `user_id` in the profile table serves as a foreign key that references the user table. To enforce uniqueness, you can declare it as unique:

```sql
CREATE TABLE users (
  user_id SERIAL PRIMARY KEY,
  username VARCHAR(50),
  email VARCHAR(100)
);

CREATE TABLE profiles (
  profile_id SERIAL PRIMARY KEY,
  user_id INTEGER REFERENCES users(user_id) UNIQUE,
  bio TEXT
);
```

Using a one-to-one relationship ensures that data is organized without redundancy, maintaining data integrity across tables.

## One-to-Many Relationship

A **one-to-many relationship** occurs when a single record in one table (the parent table) can be associated with multiple records in another table (the child table).

Consider a **customer** table and an **order** table:

- **Customer Table**:
  - customer_id (Primary Key)
  - name
  - email
- **Order Table**:
  - order_id (Primary Key)
  - order_date
  - customer_id (Foreign Key)

A customer can place multiple orders, while each order is linked to one specific customer.

```sql
CREATE TABLE customers (
  customer_id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  email VARCHAR(100)
);

CREATE TABLE orders (
  order_id SERIAL PRIMARY KEY,
  order_date DATE,
  customer_id INTEGER REFERENCES customers(customer_id)
);
```

This relationship allows for efficient data organization without redundancy, enabling a clear representation of how customers interact with their orders.

## Many-to-Many Relationship

A **many-to-many relationship** occurs when multiple records in one table can relate to multiple records in another table. This relationship typically requires a third table, known as a join or cross-reference table, to manage the associations.

Consider a **student** table and a **course** table:

- **Student Table**:
  - student_id (Primary Key)
  - name
- **Course Table**:
  - course_id (Primary Key)
  - title

To establish a many-to-many relationship, create a **registration** table:

- **Registration Table**:
  - student_id (Foreign Key)
  - course_id (Foreign Key)
  - PRIMARY KEY (student_id, course_id)

```sql
CREATE TABLE students (
  student_id SERIAL PRIMARY KEY,
  name VARCHAR(100)
);

CREATE TABLE courses (
  course_id SERIAL PRIMARY KEY,
  title VARCHAR(100)
);

CREATE TABLE registrations (
  student_id INTEGER REFERENCES students(student_id),
  course_id INTEGER REFERENCES courses(course_id),
  PRIMARY KEY (student_id, course_id)
);
```

The registration table allows for tracking which students are enrolled in which courses without redundancy. It efficiently manages the many-to-many relationships between the two entities.
