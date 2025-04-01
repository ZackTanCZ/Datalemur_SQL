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

## [Question 02]()
<details>
  <summary>SQL Query</summary>

  ```
  
  ```
</details>

<details>
  <summary>Comments</summary>

</details>

## [Question 03]()
<details>
  <summary>SQL Query</summary>

  ```
  
  ```
</details>

<details>
  <summary>Comments</summary>

</details>

## [Question 04]()
<details>
  <summary>SQL Query</summary>

  ```
  
  ```
</details>

<details>
  <summary>Comments</summary>

</details>

## [Question 05]()
<details>
  <summary>SQL Query</summary>

  ```
  
  ```
</details>

<details>
  <summary>Comments</summary>

</details>

## [Question 06]()
<details>
  <summary>SQL Query</summary>

  ```
  
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
