# [DataLemur SQL Interview Questions (Easy)](https://datalemur.com/questions?category=SQL)

## [Question 01](https://datalemur.com/questions/sql-histogram-tweets)
<details>
  <summary>SQL Query</summary>

  ```
SELECT tblCount.tweets AS "tweet_bucket", COUNT(*) AS "user_num"
FROM (
SELECT user_id , COUNT(*) as "tweets"
FROM tweets
WHERE tweet_date BETWEEN '2022-01-01' AND '2022-12-31'
GROUP BY user_id
) AS tblCount
GROUP BY tblCount.tweets
  ```
</details>

## [Question 02](https://datalemur.com/questions/matching-skills)
<details>
  <summary>SQL Query</summary>

  ```
SELECT candidate_id
FROM (
SELECT candidate_id, COUNT(skill) as skill_num 
FROM candidates
WHERE skill IN ('Python', 'Tableau','PostgreSQL')
GROUP BY candidate_id) AS skilltbl
WHERE skilltbl.skill_num = 3
  ```
</details>

## [Question 03](https://datalemur.com/questions/sql-page-with-no-likes)
<details>
  <summary>SQL Query</summary>

  ```
SELECT p.page_id AS pageID
FROM pages AS p
LEFT JOIN page_likes as pl
ON p.page_id = pl.page_id
WHERE pl.liked_date ISNULL
ORDER BY p.page_id ASC;
  ```
</details>

## [Question 04](https://datalemur.com/questions/tesla-unfinished-parts)
<details>
  <summary>SQL Query</summary>

  ```
SELECT part, assembly_step 
FROM parts_assembly
WHERE finish_date ISNULL;
  ```
</details>

## [Question 05](https://datalemur.com/questions/laptop-mobile-viewership)
<details>
  <summary>SQL Query</summary>

  ```
SELECT 
SUM(CASE 
WHEN device_type = 'laptop' THEN 1 ELSE 0 END) AS "Laptop_Views",
SUM(CASE
WHEN device_type = 'phone' THEN 1
WHEN device_type = 'tablet' THEN 1
ELSE 0 END) AS "Mobile_Views"
FROM viewership;
  ```
</details>

<details>
  <summary>Comments</summary>

  > use `CASE` Statement to swtich between different type of viewership

</details>

## [Question 06](https://datalemur.com/questions/sql-average-post-hiatus-1)
<details>
  <summary>SQL Query</summary>

  ```
SELECT user_id,
-- COUNT(user_id),
-- MAX(post_date::DATE),
-- MIN(post_date::DATE),
(MAX(post_date::DATE) - MIN(post_date::DATE)) AS "days_between"
FROM posts
WHERE DATE_PART('YEAR', post_date) = '2021'
GROUP BY user_id
HAVING COUNT(user_id) >= 2;
  ```
</details>

<details>
  <summary>Comments</summary>

> Use `MIN()` & `MAX()` functions to find the first date and last date in 2021 for each user

> Use `DATE_PART()` to extract the year element from the `post_date` column

> Filter away users with lesser than 2 posts with the `HAVING` clause

</details>

## [Question 07](https://datalemur.com/questions/teams-power-users)
<details>
  <summary>SQL Query</summary>

  ```
SELECT msg.sender_id,
COUNT(msg.message_id) AS "msg_count"
FROM messages AS msg
WHERE DATE_PART('MONTH', sent_date) = 8 AND 
DATE_PART('YEAR', sent_date) = '2022' 
GROUP BY msg.sender_id
ORDER BY COUNT(msg.message_id) DESC
LIMIT 2;
  ```
</details>

<details>
  <summary>Comments</summary>



</details>

## [Question 08](https://datalemur.com/questions/duplicate-job-listings)
<details>
  <summary>SQL Query</summary>

  ```
SELECT COUNT(*) AS "duplicate_companies"
FROM(
SELECT company_id
FROM job_listings
GROUP BY company_id, title, description
HAVING COUNT(*) >= 2
) AS "duptbl"

  ```
</details>

<details>
  <summary>Comments</summary>



</details>

## [Question 09](https://datalemur.com/questions/completed-trades)
<details>
  <summary>SQL Query</summary>

  ```
SELECT 
u.city,
COUNT(t.order_id) AS "total_orders"
FROM trades AS "t"
JOIN users AS "u"
ON t.user_id = u.user_id 
WHERE t.status = 'Completed'
GROUP BY u.city
ORDER BY COUNT(t.order_id) DESC
LIMIt 3;
  ```
</details>

<details>
  <summary>Comments</summary>



</details>



## [Question 10](https://datalemur.com/questions/sql-avg-review-ratings)
<details>
  <summary>SQL Query</summary>

  ```
SELECT
DATE_PART('MONTH', r.submit_date) AS "mth",
r.product_id,
ROUND(AVG(r.stars),2) AS "avg_stars"
FROM reviews AS "r"
GROUP BY DATE_PART('MONTH', r.submit_date),r.product_id
ORDER BY DATE_PART('MONTH', r.submit_date), r.product_id;
  ```
</details>

<details>
  <summary>Comments</summary>



</details>


## [Question 11](https://datalemur.com/questions/sql-well-paid-employees)
<details>
  <summary>SQL Query</summary>

  ```
SELECT 
employee_id,
name
FROM(SELECT
e.employee_id,
e.name,
e.salary,
e.manager_id,
m.salary,
(CASE WHEN e.salary > m.salary THEN 1 ELSE 0 END) AS "over_paid"
FROM employee AS "e"
LEFT JOIN employee AS "m"
ON e.manager_id = m.employee_id
WHERE e.manager_id IS NOT NULL
) AS "salarytbl"
WHERE salarytbl.over_paid = 1
ORDER BY employee_id
LIMIT 5
  ```
</details>

<details>
  <summary>Comments</summary>

> Query is probably not optimised

> A simpler query is to add `e.salary > m.salary` in the `WHERE` clause instead

</details>



## [Question 12](https://datalemur.com/questions/click-through-rate)
<details>
  <summary>SQL Query</summary>

  ```
SELECT 
app_id,
ROUND((100.0 * SUM(CASE WHEN event_type = 'click' THEN 1 ELSE 0 END)/
SUM(CASE WHEN event_type = 'impression' THEN 1 ELSE 0 END)),2) AS "CTR"
FROM events
WHERE DATE_PART('YEAR', timestamp) = '2022'
GROUP BY app_id

  ```
</details>

<details>
  <summary>Comments</summary>

> SubQuery can also be used to solve this problem

</details>



## [Question 13](https://datalemur.com/questions/second-day-confirmation)
<details>
  <summary>SQL Query</summary>

  ```
SELECT 
e.user_id
-- e.signup_date,
-- MIN(t.action_date::DATE),
-- MAX(t.action_date::DATE),
-- MAX(t.action_date::DATE) - MIN(t.action_date::DATE) AS "diff"
FROM emails AS "e"
JOIN texts AS "t"
ON e.email_id = t.email_id
GROUP BY e.user_id
HAVING MAX(t.action_date::DATE) - MIN(t.action_date::DATE) = 1;
  ```
</details>

<details>
  <summary>Comments</summary>

</details>








