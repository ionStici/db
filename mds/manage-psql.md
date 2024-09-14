# Installing and Managing PostgreSQL Locally

## Table of Contents

- [Installation and Access](#installation-and-access)
- [Managing Databases](#managing-databases)
- [Managing Users and Roles](#managing-users-and-roles)
- [Managing Tables](#managing-tables)
- [Backing Up and Restoring Databases](#backing-up-and-restoring-databases)
- [Get Help](#get-help)
- [PostgreSQL GUIs](#postgresql-guis)

## Installation and Access

[PostgreSQL](https://www.postgresql.org) is a powerful, open-source, object-relational database system with over 30 years of active development that has earned it a strong reputation for reliability, feature robustness, and performance.

```bash
# Install
brew install postgresql@16

# Start PostgreSQL Server (background service)
brew services start postgresql@16

# Stop PostgreSQL Server
brew services stop postgresql@16

# Verify the Installation
psql --version

# Access PostgreSQL
psql postgres
```

- `psql` : tool is a command-line interface to interact with PostgreSQL.
- `postgres` : is the default database created during installation.

## Managing Databases

```sql
-- Check current database connection
\conninfo

-- Create Database
CREATE DATABASE database_name;

-- List all databases in the PostgreSQL instance
\l

-- Connect to a Database
\c database_name;

-- Come back
\c postgres

-- Dropping a Database
DROP DATABASE database_name;

-- Clear the Screen
\! clear

-- Exit 'psql' session
\q
```

## Managing Users and Roles

PostgreSQL uses **roles** to manage authentication and permissions. Roles can be **superusers** or have more restricted privileges.

```sql
-- Create a new User
CREATE ROLE user_name WITH LOGIN PASSWORD 'your_password';

-- Granting Superuser Privileges (full control over the database)
ALTER ROLE user_name WITH SUPERUSER;

-- List Users (Roles)
\du

-- Grant Specific Privileges
GRANT ALL PRIVILEGES ON DATABASE database_name TO user_name;

-- Delete a User (Role) from PostgreSQL
DROP ROLE user_name;
```

## Managing Tables

```sql
-- Create a Table inside a Database
CREATE TABLE friends (id INTEGER PRIMARY KEY, name TEXT NOT NULL);

-- List tables in the Current Database
\dt

-- Describe a Table's Structure
\d table_name

-- With Extended Information
\d+ table_name
```

## Backing Up and Restoring Databases

PostgreSQL provides tools for backing up and restoring databases. These operations are done outside `psql` using the command line.

```bash
# Backup a Database
pg_dump database_name > test_db_backup.sql

# Restore a Database
psql database_name < test_db_backup.sql
```

## Get Help

```sql
-- List all SQL Commands
\h

-- Help on a Specific SQL Command
\h CREATE DATABASE
```

## PostgreSQL GUIs

- [Postbird](https://github.com/Paxa/postbird)
- [pbAdmin](https://www.pgadmin.org)
