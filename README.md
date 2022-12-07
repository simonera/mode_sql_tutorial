# Mode SQL tutorial
In this repository, I am saving all the SQL queries from the [Mode tutorial](https://mode.com/sql-tutorial/). It's a *work in progress*.

## [Basic SQL](https://mode.com/sql-tutorial/introduction-to-sql/)

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

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  artist IN ('M.C. Hammer', 'Hammer', 'Elvis Presley')
```

### [BETWEEN](https://mode.com/sql-tutorial/sql-between/)

`BETWEEN` is a logical operator that allows you to select only rows that are within a specific range. It has to be paired with `AND`:

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  year_rank BETWEEN 5
  AND 10
```

`BETWEEN` includes the range bounds (in this case, 5 and 10) that you specify.

#### Practice Problem

Write a query that shows all top 100 songs from January 1, 1985 through December 31, 1990.

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  year BETWEEN 1985
  AND 1990
```

### [IS NULL](https://mode.com/sql-tutorial/sql-is-null/)

`IS NULL` allows you to exclude rows with missing data:

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  artist IS NULL
```

#### Practice Problem

Write a query that shows all of the rows for which `song_name` is null.

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  song_name IS NULL
```

### [AND](https://mode.com/sql-tutorial/sql-and-operator/)

`AND` allows you to select only rows that satisfy two conditions. The following query will return all rows for top-10 recordings in 2012:

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  year = 2012
  AND year_rank <= 10
```

You can use `AND` as many times as you want:

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  year = 2012
  AND year_rank <= 10
  AND "group" ILIKE '%feat%'
```

#### Practice Problem 1

Write a query that surfaces all rows for top-10 hits for which Ludacris is part of the Group.

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  "group" ILIKE '%ludacris%'
  AND year_rank <= 10
```

#### Practice Problem 2

Write a query that surfaces the top-ranked records in 1990, 2000, and 2010.

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  year_rank = 1
  AND year IN (1990, 2000, 2010)
```

#### Practice Problem 3

Write a query that lists all songs from the 1960s with "love" in the title.

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  year BETWEEN 1960 AND 1969
  AND song_name ILIKE '%love%'
```

### [OR](https://mode.com/sql-tutorial/sql-or-operator/)

`OR` allows you to select rows that satisfy either of two conditions:

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  year_rank = 5
  OR artist = 'Gotye'
```

You can combine AND with OR using parenthesis:

```
SELECT *
  FROM tutorial.billboard_top_100_year_end
 WHERE year = 2013
   AND ("group" ILIKE '%macklemore%' OR "group" ILIKE '%timberlake%')
```

#### Practice Problem 1

Write a query that returns all rows for top-10 songs that featured either Katy Perry or Bon Jovi.

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  year_rank <= 10
  AND ("group" ILIKE '%katy perry%' OR "group" ILIKE '%bon jovi%')
```

#### Practice Problem 2

Write a query that returns all songs with titles that contain the word "California" in either the 1970s or 1990s.

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  song_name ILIKE '%california%'
  AND (year BETWEEN 1970 AND 1979 OR year BETWEEN 1990 AND 1999)
```

#### Practice Problem 3

Write a query that lists all top-100 recordings that feature Dr. Dre before 2001 or after 2009.

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  "group" ILIKE '%dr. dre%'
  AND (year < 2001 OR year > 2009)
```

Alternatively:

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  "group" ILIKE '%dr. dre%'
  AND (year <= 2000 OR year >= 2010)
```

### [NOT](https://mode.com/sql-tutorial/sql-not-operator/)

You can put `NOT` before any conditional statement to select rows for which that statement is false:

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  year = 2013
  AND year_rank NOT BETWEEN 2 AND 3
```

`NOT` is commonly used with `LIKE`. Run this query and check out how Macklemore magically disappears!

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  year = 2013
  AND "group" NOT ILIKE '%macklemore%'
```

NOT is also frequently used to identify non-null rows, but the syntax is somewhat special—you need to include IS beforehand. Here's how that looks:

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  year = 2013
  AND artist IS NOT NULL
```

#### Practice Problem

Write a query that returns all rows for songs that were on the charts in 2013 and do not contain the letter "a".

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  year = 2013
  AND song_name NOT ILIKE '%a%'
```

### [ORDER BY](https://mode.com/sql-tutorial/sql-order-by/)

Once you've learned how to filter data, it's time to learn how to sort data. `ORDER BY` allows you to reorder your results based on the data in one or more columns. The ascending order is the default:

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
ORDER BY
  artist
```

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  year = 2013
ORDER BY
  year_rank
```

If you want the descending order, add `DESC`:

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  year = 2013
ORDER BY
  year_rank DESC
```

#### Practice Problem 1

Write a query that returns all rows from 2012, ordered by song title from Z to A.

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  year = 2012
ORDER BY
  song_name DESC
```

You can also order by mutiple columns:

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  year_rank <= 3
ORDER BY
  year DESC, year_rank
```

#### Practice Problem 2

Write a query that returns all rows from 2010 ordered by rank, with artists ordered alphabetically for each song.

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  year = 2010
ORDER BY
  year_rank, artist
```

You can "comment out" pieces of code by adding combinations of characters, for example: `--` (two dashes) to comment out everything to the right of them on a given line, and `/*` ... `*/` to comment across multiple lines.

#### Practice Problem 3

Write a query that shows all rows for which T-Pain was a group member, ordered by rank on the charts, from lowest to highest rank (from 100 to 1).

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  "group" ILIKE '%t-pain%'
ORDER BY
  year_rank DESC
```

#### Practice Problem 4

Write a query that returns songs that ranked between 10 and 20 (inclusive) in 1993, 2003, or 2013. Order the results by year and rank, and leave a comment on each line of the WHERE clause to indicate what that line does

```
SELECT
  *
FROM
  tutorial.billboard_top_100_year_end
WHERE
  year_rank BETWEEN 10 AND 20 -- returns songs that ranked between 10 and 20 
  AND year IN (1993, 2003, 2013) -- returns songs from 1993, 2003, or 2013
ORDER BY
  year, year_rank
```

This is for the basic SQL tutorial. Next: the intermediate level!

## [Intermediate SQL](https://mode.com/sql-tutorial/intro-to-intermediate-sql/)

### [Aggregate Functions](https://mode.com/sql-tutorial/sql-aggregate-functions/)

SQL is excellent at aggregating data the way you might in a pivot table in Excel. You will use aggregate functions all the time, so it's important to get comfortable with them:

* `COUNT` counts how many rows are in a particular column.
* `SUM` adds together all the values in a particular column.
* `MIN` and `MAX` return the lowest and highest values in a particular column, respectively.
* `AVG` calculates the average of a group of selected values.

While arithmetic operators only perform operations across rows, aggregate functions are used to perform operations across entire columns (which could include millions of rows of data or more).

### [COUNT](https://mode.com/sql-tutorial/sql-count/)

#### Counting all rows

```
SELECT
  COUNT(*)
FROM
  tutorial.aapl_historical_stock_price
```

#### Counting individual columns

The following code will provide a count of all of rows in which the `high` column **is not null**:

```
SELECT COUNT(high)
  FROM tutorial.aapl_historical_stock_price
```

#### Practice Problem 1

Write a query to count the number of non-null rows in the low column.

```
SELECT
  COUNT(low)
FROM
  tutorial.aapl_historical_stock_price
```

#### Counting non-numerical columns

One nice thing about `COUNT` is that you can use it on non-numerical columns:

```
SELECT
  COUNT(date)
FROM
  tutorial.aapl_historical_stock_price
```

You can also use an alias:

```
SELECT
  COUNT(date) AS count_of_date
FROM
  tutorial.aapl_historical_stock_price
```

IF you must USE spaces, you will need TO USE double quotes:

```
SELECT
  COUNT(date) AS "Count Of Date"
FROM
  tutorial.aapl_historical_stock_price
```

#### Practice Problem 2

Write a query that determines counts of every single column. With these counts, can you tell which column has the most null values?

```
SELECT
  COUNT(date) AS count_of_date,
  COUNT(year) AS count_of_year,
  COUNT(month) AS count_of_month,
  COUNT(open) AS count_of_open,
  COUNT(high) AS count_of_high,
  COUNT(low) AS count_of_low,
  COUNT(close) AS count_of_close,
  COUNT(volume) AS count_of_volume,
  COUNT(id) AS count_of_id
FROM
  tutorial.aapl_historical_stock_price
```

### [SUM](https://mode.com/sql-tutorial/sql-sum/)

`SUM` totals the values in a given column. Unlike `COUNT`, you can only use `SUM` on columns containing numerical values:

```
SELECT
  SUM(volume)
FROM
  tutorial.aapl_historical_stock_price
```

`SUM` treats nulls as 0, so don't worry about them.

#### Practice Problem

Write a query to calculate the average opening price (hint: you will need to use both COUNT and SUM, as well as some simple arithmetic).

```
SELECT
  SUM(OPEN) / COUNT(OPEN) AS avg_open,
FROM
  tutorial.aapl_historical_stock_price
```

### [MIN/MAX](https://mode.com/sql-tutorial/sql-min-max/)

`MIN` and `MAX` return the lowest and highest values in a particular column. They can be used on non-numerical columns. For example, `MIN` will return the lowest number, earliest date, or non-numerical value as close alphabetically to "A" as possible:

```
SELECT
  MIN(volume) AS min_volume,
  MAX(volume) AS max_volume
FROM
  tutorial.aapl_historical_stock_price
```

#### Practice Problem 1

What was Apple's lowest stock price (at the time of this data collection)?

```
SELECT
  MIN(low) AS min_low
FROM
  tutorial.aapl_historical_stock_price
```

Answer: 6.36. 

#### Practice Problem 2

What was the highest single-day increase in Apple's share value?

```
SELECT
  MAX(close-open) AS max_increase
FROM
  tutorial.aapl_historical_stock_price
```
Answer: 32.58.

### [AVG](https://mode.com/sql-tutorial/sql-avg/)

`AVG` calculates the average of a selected group of values. It's very useful, but has some limitations. First, it can only be used on numerical columns. Second, it ignores nulls completely. There are some cases in which you'll want to treat null values as 0. For these cases, you'll want to write a statement that changes the nulls to 0 (covered in a later lesson). 

#### Practice Problem

Write a query that calculates the average daily trade volume for Apple stock.

```
SELECT
  AVG(volume) AS avg_volume
FROM
  tutorial.aapl_historical_stock_price
```

### [GROUP BY](https://mode.com/sql-tutorial/sql-group-by/)

`COUNT`, `AVG`, and `SUM` have something in common: they all aggregate across the entire table. If you want to aggregate only part of a table, use `GROUP BY`. `GROUP BY` allows you to separate data into groups, which can be aggregated independently of one another.

```
SELECT
  year,
  COUNT(*) AS count
FROM
  tutorial.aapl_historical_stock_price
GROUP BY
  year
```

To group by multiple columns, add a comma:

```
SELECT
  year,
  month,
  COUNT(*) AS count
FROM
  tutorial.aapl_historical_stock_price
GROUP BY
  year,
  month
```

#### Practice Problem 1

Calculate the total number of shares traded each month. Order your results chronologically.

```
SELECT
  year,
  month,
  SUM(volume) AS sum_volume
FROM
  tutorial.aapl_historical_stock_price
GROUP BY
  year, month
ORDER BY
  year, month
```

#### Practice Problem 2

Write a query to calculate the average daily price change in Apple stock, grouped by year.

```
SELECT
  year, 
  AVG(close-open) AS avg_price_change
FROM
  tutorial.aapl_historical_stock_price
GROUP BY
  year
ORDER BY
  year
```

#### Practice Problem 3

Write a query that calculates the lowest and highest prices that Apple stock achieved each month.

```
SELECT
  year, 
  month, 
  MIN(low) AS lowest,
  MAX(high) AS highest
FROM
  tutorial.aapl_historical_stock_price
GROUP BY
  year, month
ORDER BY
  year, month
```
