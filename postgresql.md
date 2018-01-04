# PostgreSQL

> The definitive SQL database.

## Create Database
```sql
CREATE DATABASE dbname;
```

## Create Table
With auto numbering integer id.
```sql
CREATE TABLE tablename (
 id serial PRIMARY KEY,
 name varchar(50) UNIQUE NOT NULL,
 dateCreated timestamp DEFAULT current_timestamp
);
```

## Add a Primary Key
```sql
ALTER TABLE tableName ADD PRIMARY KEY (id);
```

## Create an Index
```sql
CREATE UNIQUE INDEX indexName ON tableName (columnNames);
```

## Backup a Database
```sql
pg_dump dbName > dbName.sql
```

## Backup all Databases
```sql
pg_dumpall > pgbackup.sql
```

## Run SQL Script
```sql
psql -f script.sql databasename
```

## Search Using a Regular Expression
```sql
SELECT column FROM table WHERE column ~ 'foo.*';
```

## The First n Records
```sql
SELECT columns FROM table LIMIT 10;
```

## Pagination
```sql
SELECT cols FROM table LIMIT 10 OFFSET 30;
```

## Prepared Statements
```sql
PREPARE preparedInsert (int, varchar) AS
  INSERT INTO tableName (intColumn, charColumn) VALUES ($1, $2);
EXECUTE preparedInsert (1,'a');
EXECUTE preparedInsert (2,'b');
DEALLOCATE preparedInsert;
```

## Create a Function
```sql
CREATE OR REPLACE FUNCTION month (timestamp) RETURNS integer 
 AS 'SELECT date_part(''month'', $1)::integer;'
LANGUAGE 'sql';
```

## Table Maintenance
```sql
VACUUM ANALYZE table;
```

## Reindex a Database, Table or Index
```sql
REINDEX DATABASE dbName;
```

## Show query plan
```sql
EXPLAIN SELECT * FROM table;
```

## Import from a File
```sql
COPY destTable FROM '/tmp/somefile';
```

## Show all Runtime Parameters
```sql
SHOW ALL;
```

## Grant all Permissions to a User
```sql
GRANT ALL PRIVILEGES ON table TO username;
```

## Perform a Transaction
```sql
BEGIN TRANSACTION 
 UPDATE accounts SET balance += 50 WHERE id = 1;
COMMIT;
```

## Get all Columns and Rows from a Table
```sql
SELECT * FROM table;
```

## Add a new row
```sql
INSERT INTO table (column1,column2)
VALUES (1, 'one');
```

## Update a row
```sql
UPDATE table SET foo = 'bar' WHERE id = 1;
```

## Delete a row
```sql
DELETE FROM table WHERE id = 1;
```

## Client Application Usage

* https://www.postgresql.org/docs/current/static/app-psql.html
