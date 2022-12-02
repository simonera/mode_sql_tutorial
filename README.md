# Mode SQL tutorial
Here I save the SQL queries from the [Mode tutorial](https://mode.com/sql-tutorial/).

## Basic SQL

### SELECT

Practice problem 1
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

Practice problem 2
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
