# Mode SQL tutorial
In this repository, I am saving all the SQL queries from the [Mode tutorial](https://mode.com/sql-tutorial/). It's a *work in progress*.

## Basic SQL

### [SELECT](https://mode.com/sql-tutorial/sql-select-statement/)

#### Practice problem 1

Write a query to select all of the columns in the `tutorial.us_housing_units` table without using `*`.

```
SELECT
  year,
  month,
  month_name,
  south,
  west,
  midwest,
  northeast
FROM
  tutorial.us_housing_units
```

#### Practice problem 2

Write a query to select all of the columns in `tutorial.us_housing_units` and rename them so that their first letters are capitalized.

```
SELECT
  year AS "Year",
  month AS "Month",
  month_name AS "Month Name",
  south AS "South",
  west AS "West",
  midwest AS "Midwest",
  northeast AS "Northest"
FROM
  tutorial.us_housing_units
```

### [LIMIT](https://mode.com/sql-tutorial/sql-limit/)

Write a query that uses the `LIMIT` command to restrict the result set to only 15 rows.

```
SELECT
  *
FROM
  tutorial.us_housing_units
LIMIT
  15
```

### [WHERE](https://mode.com/sql-tutorial/sql-where/)
```
SELECT
  *
FROM
  tutorial.us_housing_units
WHERE
  month = 1
```

### [Comparison Operators](https://mode.com/sql-tutorial/sql-operators/)

| Comparison | Operator |
| ----------- | ----------- |
| Equal to	| = |
| Not equal to	| <> or != |
| Greater than	| > |
| Less than	| < |
| Greater than or equal to | >= |
| Less than or equal to	| <= |

For non-numerical data, use single quotes: ` WHERE month_name != 'January'` 

Greater-than and less-than operators (`>`, `<`, `>=`, or `<=`) sort by alphabetic order: `WHERE month_name > 'J'`

#### Practice problem 1

Did the West Region ever produce more than 50,000 housing units in one month?

```
SELECT
  *
FROM
  tutorial.us_housing_units
WHERE
  west > 50
```

Answer: yes, 3 times. 

#### Practice problem 2

Did the South Region ever produce 20,000 or fewer housing units in one month?

```
SELECT
  *
FROM
  tutorial.us_housing_units
WHERE
  south <= 20
```

Answer: yes, 4 times. 

#### Practice problem 3

Write a query that only shows rows for which the month name is February.

```
SELECT
  *
FROM
  tutorial.us_housing_units
WHERE
  month_name = 'February'
```

#### Practice problem 4

Write a query that only shows rows for which the `month_name` starts with the letter "N" or an earlier letter in the alphabet.

```
SELECT
  *
FROM
  tutorial.us_housing_units
WHERE
  month_name < 'o'
```

#### Practice problem 5

Write a query that calculates the sum of all four regions in a separate column.

```
SELECT
  year,
  month,
  south,
  west,
  midwest,
  northeast
  south + west + midwest + northeast AS usa_total
FROM
  tutorial.us_housing_units
```

#### Practice problem 6

Write a query that returns all rows for which more units were produced in the West region than in the Midwest and Northeast combined.

```
SELECT
  year,
  month,
  south,
  west,
  midwest,
  northeast
FROM
  tutorial.us_housing_units
WHERE
  west > (midwest + northeast)
```

#### Practice problem 7

Write a query that calculates the percentage of all houses completed in the United States represented by each region. Only return results from the year 2000 and later.

```
SELECT
  year,
  month,
  south / (south + west + midwest + northeast) * 100 AS perc_south,
  west / (south + west + midwest + northeast) * 100 AS perc_west,
  midwest / (south + west + midwest + northeast) * 100 AS perc_midwest,
  northeast / (south + west + midwest + northeast) * 100 AS perc_northeast
FROM
  tutorial.us_housing_units
WHERE
  year >= 2000
```

### [Logical Operators](https://mode.com/sql-tutorial/sql-logical-operators/)

Logical operators allow you to use multiple comparison operators in one query. 

* `LIKE` allows you to match similar values, instead of exact values.
* `IN` allows you to specify a list of values you'd like to include.
* `BETWEEN` allows you to select only rows within a certain range.
* `IS NULL` allows you to select rows that contain no data in a given column.
* `AND` allows you to select only rows that satisfy two conditions.
* `OR` allows you to select rows that satisfy either of two conditions.
* `NOT` allows you to select rows that do not match a certain condition.

### [LIKE](https://mode.com/sql-tutorial/sql-like/)

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  "group" LIKE 'Snoop%'
```

Note: "group" is between double quotes to indicate that it is a column (instead of the `GROUP` command). `%` is a wildcard, which represents any character or set of characters. 

`LIKE` is case-sensitive. To ignore case, use `ILIKE`:

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  "group" ILIKE 'snoop%'
```

You can also use `_` (a single underscore) to substitute for an individual character:

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  artist ILIKE 'dr_ke'
```

#### Practice Problem 1

Write a query that returns all rows for which Ludacris was a member of the group.

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  "group" ILIKE '%ludacris%'
```

#### Practice Problem 2

Write a query that returns all rows for which the first artist listed in the group has a name that begins with "DJ".

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  "group" LIKE 'DJ%'
```

### [IN](https://mode.com/sql-tutorial/sql-in-operator/)

The following query will return results for which the `year_rank` column is equal to one of the values in the list:

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  year_rank IN (1, 2, 3)
```

The values in the list must be separated by commas. 

As with comparison operators, you can use non-numerical values, but they need to go inside single quotes:

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  artist IN ('Taylor Swift', 'Usher', 'Ludacris')
```

#### Practice Problem

Write a query that shows all of the entries for Elvis and M.C. Hammer.

