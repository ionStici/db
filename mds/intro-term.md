# Introductory Terminology

## Database

A **database** is a **structured collection of data** that is stored, managed, and accessed via a computer system. It allows for the efficient **storage, retrieval, and manipulation** of data. Typically, databases are managed by **Database Management Systems (DBMS)**, which provide interfaces for interacting with the data. These systems allow for operations such as **querying, updating**, and **managing** data in a structured way.

## Relational Database

A **relational database** is a type of database that stores data in a **structured format using tables** (also referred to as **relations**). Each table is composed of **rows** (records) and **columns** (attributes), where each **row** represents a unique entry, and each **column** represents a specific data field, typically of a designated **data type** (e.g. `INTEGER`, `TEXT`, `DATE`).

**Example:** A table called `employees` might contain columns such as `id`, `name`, and `age`. The `id` column would be an `INTEGER` used to uniquely identify each employee.

## Relational Database Management System (RDBMS)

A **Relational Database Management System (RDBMS)** is a software program that allows users to **create, update, and manage** a relational database. Most RDBMSs use the **SQL** language to query and manipulate the data from the database. These systems ensure data integrity, support concurrent users, and enforce relationships between tables via foreign keys.

Examples of RDBMS include **MySQL**, **PostgreSQL**, **SQLite**, **Oracle Database**, and **Microsoft SQL Server**.

## SQL (Structured Query Language)

**SQL (Structured Query Language)** is the **standard programming language** used to communicate with data stored in a relational database management system. SQL allows for a variety of operations including **querying**, **inserting**, **updating**, and **deleting** data.

Common SQL-based database systems:

- **MySQL** : One of the most widely used open-source SQL databases, particularly popular for web applications. It is often paired with PHP in the LAMP (Linux, Apache, MySQL, PHP) stack.

- **PostgreSQL** : A powerful, open-source SQL database known for its adherence to SQL standards, advanced features (e.g., support for JSON, indexing, and stored procedures), and extensibility. PostgreSQL is commonly used for web applications and data-intensive applications.

- **SQLite** : A self-contained, serverless SQL database that stores data in a single file on disk. SQLite is lightweight and frequently used in mobile applications, small desktop apps, and embedded systems due to its simplicity and local storage capability.

- **Oracle DB** : A proprietary RDBMS developed by Oracle Corporation. It is typically used for large, complex applications, particularly in enterprise and financial sectors, where high performance and security are critical.

- **SQL Server** : A proprietary RDBMS developed by Microsoft. It is used primarily for enterprise applications in Windows environments and is known for its integration with other Microsoft products like Azure and Power BI.

### Differences and Context

Each of these database systems has its own strengths and ideal use cases:

- **MySQL** : Ideal for web applications, particularly in LAMP stacks, with a strong focus on read-heavy operations.

- **PostgreSQL** : Offers more advanced features and is ideal for applications requiring complex data handling, transactions, and high concurrency.

- **SQLite** : Perfect for small, embedded applications where a serverless and lightweight solution is needed.

- **Oracle DB** : Suited for enterprise-level applications with a focus on security and scalability.

- **SQL Server** : Best for large organizations using Microsoft’s ecosystem.
