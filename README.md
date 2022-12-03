# Mode SQL tutorial
Here I save the SQL queries from the [Mode tutorial](https://mode.com/sql-tutorial/).

## Basic SQL

### [SELECT](https://mode.com/sql-tutorial/sql-select-statement/)

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

### [LIMIT](https://mode.com/sql-tutorial/sql-limit/)
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

Comparison operators on numerical data

| Comparison | Operator |
| ----------- | ----------- |
| Equal to	| = |
| Not equal to	| <> or != |
| Greater than	| > |
| Less than	| < |
| Greater than or equal to | >= |
| Less than or equal to	| <= |

Practice problem 1
```
SELECT
  *
FROM
  tutorial.us_housing_units
WHERE
  west > 50
```

Answer: yes, 3 times. 

Practice problem 2
```
SELECT
  *
FROM
  tutorial.us_housing_units
WHERE
  south <= 20
```

Answer: yes, 4 times. 
