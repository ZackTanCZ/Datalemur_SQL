# SQL_Med

## [Question 01](https://datalemur.com/questions/sql-third-transaction)
<details>
  <summary>SQL Query</summary>

  ```
SELECT
t.user_id,
t.spend,
t.transaction_date
FROM(SELECT *,
ROW_NUMBER() OVER (PARTITION BY user_id ORDER BY transaction_date) AS "row_num"
FROM transactions) AS "t"
WHERE t.row_num = 3
  ```
</details>

<details>
  <summary>Comments</summary>

</details>

## [Question 02](https://datalemur.com/questions/sql-second-highest-salary)
<details>
  <summary>SQL Query</summary>

  ```
  WITH salaryTbl AS (
SELECT
RANK() OVER ( ORDER BY salary DESC ),
*
FROM employee
)
SELECT
salaryTbl.salary AS "second_highest_salary"
FROM salaryTbl
WHERE salaryTbl.rank = 2
  ```
</details>

<details>
  <summary>Comments</summary>

> Use CTE to include a ranking column

> Filter to rank 2 for second highest salary

</details>

## [Question 03](https://datalemur.com/questions/time-spent-snaps)
<details>
  <summary>SQL Query</summary>

  ```
  SELECT 
time_tbl.age_bucket,
ROUND((time_tbl.send_time/(time_tbl.total_time) * 100.0),2) AS send_percent,
ROUND((time_tbl.open_time/(time_tbl.total_time) * 100.0),2) AS open_percent
FROM (
SELECT 
age.age_bucket AS age_bucket,
SUM(act.time_spent) FILTER (WHERE act.activity_type = 'open') AS open_time,
SUM(act.time_spent) FILTER (WHERE act.activity_type = 'send') AS send_time,
(SUM(act.time_spent) FILTER (WHERE act.activity_type = 'open')) + 
(SUM(act.time_spent) FILTER (WHERE act.activity_type = 'send')) AS total_time
FROM activities AS act
JOIN age_breakdown AS age
ON act.user_id = age.user_id
WHERE activity_type IN ('open','send')
GROUP BY age.age_bucket) AS time_tbl
  ```
</details>

<details>
  <summary>Comments</summary>

> Use `Filter` to only sum up the time when `activity_type` is `send` or `open`

</details>

## [Question 04](https://datalemur.com/questions/rolling-average-tweets)
<details>
  <summary>SQL Query</summary>

  ```
  SELECT 
user_id,
tweet_date,
ROUND(AVG(tweet_count) OVER (PARTITION BY user_id ORDER BY tweet_date 
ROWS BETWEEN 2 PRECEDING AND CURRENT ROW),2) AS rolling_avg_3d
FROM tweets;
  ```
</details>

<details>
  <summary>Comments</summary>

</details>

## [Question 05](https://datalemur.com/questions/sql-highest-grossing)
<details>
  <summary>SQL Query</summary>

  ```
  SELECT 
catTbl.category,
catTbl.product,
catTbl.total_spend
FROM (SELECT
category,
product,
SUM(spend) AS total_spend,
RANK() OVER (PARTITION BY category ORDER BY SUM(spend) DESC) AS rank
FROM product_spend
WHERE DATE_PART('YEAR',transaction_date) = 2022
GROUP BY category, product
ORDER BY category) AS catTbl
WHERE catTbl.rank <= 2
  ```
</details>

<details>
  <summary>Comments</summary>

</details>

## [Question 06](https://datalemur.com/questions/sql-top-three-salaries)
<details>
  <summary>SQL Query</summary>

  ```
  SELECT
salaryTbl.dept AS department_name,
salaryTbl.name,
salaryTbl.salary
FROM (
SELECT
d.department_name AS dept,
e.name,
e.salary,
DENSE_RANK() OVER(PARTITION BY d.department_name ORDER BY e.salary DESC) AS rank
FROM employee AS e
JOIN department AS d
ON e.department_id = d.department_id
ORDER BY d.department_name ASC, rank ASC, e.name ASC) as salaryTbl
WHERE salaryTbl.rank <= 3
  ```
</details>

<details>
  <summary>Comments</summary>

</details>

## [Question 07]()
<details>
  <summary>SQL Query</summary>

  ```
  
  ```
</details>

<details>
  <summary>Comments</summary>

</details>

## [Question 08]()
<details>
  <summary>SQL Query</summary>

  ```
  
  ```
</details>

<details>
  <summary>Comments</summary>

</details>

## [Question 09]()
<details>
  <summary>SQL Query</summary>

  ```
  
  ```
</details>

<details>
  <summary>Comments</summary>

</details>

## [Question 10]()
<details>
  <summary>SQL Query</summary>

  ```
  
  ```
</details>

<details>
  <summary>Comments</summary>

</details>
