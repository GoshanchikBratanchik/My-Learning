# My cheat sheet for SQl queries
You can write in low register

SELECT <any columns or * for all columns>
SELECT DISTINCT <any columns> - delete all row with duplicate column
FROM <name of table>
WHERE <condition> 
  AND/OR <another condition> 
Condition can me standart numerical operators, col_name before all of them -> (NOT) BETWEEN ... AND ..., (NOT) IN (any numbres) 

You can compare strings:
Case insensitive exact string comparison (NOT) LIKE
Use %string% to find string in string(only with (NOT) LIKE)
Use string_ to match a single character(only with (NOT) LIKE), col_name LIKE 'AN_', match 'AND', but not AN

ORDER BY ASC/DESC - when an ORDER BY clause is specified, each row is sorted alpha-numerically based on the specified column's value
LIMIT num_limit OFFSET num_offset - the LIMIT will reduce the number of rows to return, and the optional OFFSET will specify where to begin counting the number rows from

INNER, LEFT, RIGHT, FULL JOIN another_table
  ON mytable-col = another_table-col
INNER JOIN - work with columns which exist in both table, other with any columns

Each database has its own supported set of mathematical, string, and date functions that can be used in a query, which you can find in their own respective docs.
For example:
SELECT particle_speed / 2.0 AS half_particle_speed
FROM physics_data
WHERE ABS(particle_position) * 10.0 > 500;

Use AS to rename
SELECT column AS better_column_name, …
FROM a_long_widgets_table_name AS mywidgets
INNER JOIN widget_sales
  ON mywidgets.id = widget_sales.widget_id;

You can use different functions
SELECT AGG_FUNC(column_or_expression) AS aggregate_description, …
FROM mytable
WHERE constraint_expression;
examples of functions:
COUNT(*), COUNT(column)	A common function used to counts the number of rows in the group if no column name is specified. Otherwise, count the number of rows in the group with non-NULL values in the specified column.
MIN(column)	Finds the smallest numerical value in the specified column for all rows in the group.
MAX(column)	Finds the largest numerical value in the specified column for all rows in the group.
AVG(column)	Finds the average numerical value in the specified column for all rows in the group.
SUM(column)	Finds the sum of all numerical values in the specified column for the rows in the group.

in addition to aggregating across all the rows, you can instead apply the aggregate functions to individual groups of data within that group.
The GROUP BY clause works by grouping rows that have the same value in the column specified.

write to table:
INSERT INTO boxoffice
(movie_id, rating, sales_in_millions)
VALUES (1, 9.9, 283742034 / 1000000);

UPDATE mytable
SET column = value_or_expr, 
    other_column = another_value_or_expr, 
    …
WHERE condition;

DELETE FROM mytable
WHERE condition;

One helpful tip is to always write the constraint first and test it in a SELECT query to make sure you are updating the right rows, and only then writing the column/value pairs to
update.

Use IF NOT EXIST before
CREATE TABLE IF NOT EXISTS mytable (
    column DataType TableConstraint DEFAULT default_value,
    another_column DataType TableConstraint DEFAULT default_value,
    …
);

INTEGER, BOOLEAN	The integer datatypes can store whole integer values like the count of a number or an age. In some implementations, the boolean value is just represented as an integer value of just 0 or 1.
FLOAT, DOUBLE, REAL	The floating point datatypes can store more precise numerical data like measurements or fractional values. Different types can be used depending on the floating point precision required for that value.
CHARACTER(num_chars), VARCHAR(num_chars), TEXT	
The text based datatypes can store strings and text in all sorts of locales. The distinction between the various types generally amount to underlaying efficiency of the database when working with these columns.

Both the CHARACTER and VARCHAR (variable character) types are specified with the max number of characters that they can store (longer values may be truncated), so can be more efficient to store and query with big tables.

DATE, DATETIME	SQL can also store date and time stamps to keep track of time series and event data. They can be tricky to work with especially when manipulating data across timezones.
BLOB	Finally, SQL can store binary data in blobs right in the database. These values are often opaque to the database, so you usually have to store them with the right metadata to requery them.

PRIMARY KEY	This means that the values in this column are unique, and each value can be used to identify a single row in this table.
AUTOINCREMENT	For integer values, this means that the value is automatically filled in and incremented with each row insertion. Not supported in all databases.
UNIQUE	This means that the values in this column have to be unique, so you can't insert another row with the same value in this column as another row in the table. Differs from the `PRIMARY KEY` in that it doesn't have to be a key for a row in the table.
NOT NULL	This means that the inserted value can not be `NULL`.
CHECK (expression)	This allows you to run a more complex expression to test whether the values inserted are valid. For example, you can check that values are positive, or greater than a specific size, or start with a certain prefix, etc.
FOREIGN KEY	This is a consistency check which ensures that each value in this column corresponds to another value in a column in another table.

For example, if there are two tables, one listing all Employees by ID, and another listing their payroll information, the `FOREIGN KEY` can ensure that every row in the payroll table corresponds to a valid employee in the master Employee list.

ALTER TABLE mytable
ADD column DataType OptionalTableConstraint 
    DEFAULT default_value;

ALTER TABLE mytable
DROP column_to_be_deleted;

ALTER TABLE mytable
RENAME TO new_table_name;

DROP TABLE IF EXISTS mytable;

Each database implementation supports different methods of altering their tables, so it's always best to consult your database docs before proceeding: MySQL, Postgres, SQLite, Microsoft SQL Server.

