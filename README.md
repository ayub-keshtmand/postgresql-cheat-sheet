# PostgreSQL Cheat Sheet

## Databases
Create a Database
```sql
# postgres
CREATE DATABASE databasename
```

Drop a Database
```sql
# postgres
DROP DATABASE IF EXISTS databasename
```

## Tables
Size of Table
```sql
# postgres
SELECT pg_size_pretty( pg_total_relation_size('table_name') ) ;
```

Create Schema
```sql
# postgres
CREATE SCHEMA schema_name
    CREATE TABLE table_name1 (…)
    CREATE TABLE table_name2 (...)
    CREATE VIEW view_name1
        SELECT select_list FROM table_name1;
```

Rename Table
```sql
# postgres, redshift
ALTER TABLE table_name
  RENAME TO new_table_name;

# mysql
ALTER TABLE tableName
CHANGE `oldcolname` `newcolname` datatype(length);

# mysql
RENAME TABLE old_table_name TO new_table_name;
```

Create View
```sql
CREATE VIEW view_name AS
SELECT statement ;
```

## Indexes
Create Indexes
```sql
CREATE INDEX indexname ON tablename(columnname1, columname2);
create index idx on nps(unique_customer_id, log_date);
```

Show Indexes
```sql
SELECT indexname,indexdef
FROM pg_indexes
WHERE tablename = ‘table_name';
```

## Columns
Add Column
```sql
ALTER TABLE table_name
ADD COLUMN new_column_name data_type;
```

Drop Column
```sql
ALTER TABLE table_name 
DROP COLUMN column_name ;
```

Rename Column
```sql
ALTER TABLE table_name 
RENAME COLUMN column_name TO new_column_name;
```

Change Datatype
```sql
ALTER TABLE table_name
ALTER COLUMN column_name TYPE new_data_type ;
```

## Roles
Show Roles
```sql
SELECT u.usename AS "Role name",
CASE WHEN u.usesuper AND u.usecreatedb THEN CAST('superuser, create
database' AS pg_catalog.text)
 WHEN u.usesuper THEN CAST('superuser' AS pg_catalog.text)
 WHEN u.usecreatedb THEN CAST('create database' AS
pg_catalog.text)
 ELSE CAST('' AS pg_catalog.text)
END AS "Attributes"
FROM pg_catalog.pg_user u
ORDER BY 1;
```

Drop a Role
```sql
DROP ROLE username
```

Show all Postgres processes running on machine
```bash
ps aux | grep postgres
# also shows where postgres is installed
```

## Date Diff
[How to Calculate the Difference Between Two Timestamps in PostgreSQL |   LearnSQL.com](https://learnsql.com/cookbook/how-to-calculate-the-difference-between-two-timestamps-in-postgresql/)
```sql
EXTRACT(EPOCH FROM processing_completed - request_received)
```

Old Solution
[PostgreSQL - DATEDIFF - Datetime Difference in Seconds, Days, Months, Weeks etc - SQLines Open Source Tools](http://www.sqlines.com/postgresql/how-to/datediff)
```sql
create or replace function clean_money(x varchar) returns numeric(18,2) as $$
	select replace(replace(replace(replace(x, '$',''), '£',''), 'k', ''), 'b', '')::numeric(18,2)
$$ language sql;
```

Import CSV
```sql
COPY persons(first_name, last_name, dob, email)
FROM 'C:\sampledb\persons.csv'
DELIMITER ','
CSV HEADER;
```
