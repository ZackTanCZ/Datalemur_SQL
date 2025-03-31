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

## [Question 02]()
<details>
  <summary>SQL Query</summary>

  ```

  ```
</details>
