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
