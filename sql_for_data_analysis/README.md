# SQL for Data Management and Analysis

This section demonstrates practical SQL skills for managing and analyzing data within a database context. It covers 
fundamental SQL operations, including data retrieval, filtering, joining multiple tables, and aggregation, essential 
for both data analysis and understanding system behavior.

## Scenario: User and Activity Data Analysis

We will simulate a simplified database for an application, containing two tables: `users` and `user_activity`. As a 
data analyst (or security analyst needing database insights), the goal is to query these tables to extract meaningful 
information about user registrations, login patterns, and activity types.

## Database Schema

### Table: `users`

| Column Name | Data Type | Description                    |
|-------------|-----------|--------------------------------|
| `user_id`   | INTEGER   | Unique identifier for the user |
| `username`  | TEXT      | User's chosen username         |
| `email`     | TEXT      | User's email address           |
| `reg_date`  | DATE      | Date of user registration      |

### Table: `user_activity`

| Column Name | Data Type | Description                          |
|-------------|-----------|--------------------------------------|
| `activity_id`| INTEGER   | Unique identifier for the activity |
| `user_id`   | INTEGER   | Foreign key referencing `users.user_id` |
| `activity_type`| TEXT      | Type of activity (e.g., 'login', 'logout', 'purchase', 'view_page') |
| `activity_date`| DATETIME  | Timestamp of the activity          |
| `ip_address`| TEXT      | IP address from which activity occurred |

## SQL Query Examples

Here are practical examples of SQL queries demonstrating various data management and analysis tasks.

### 1. Retrieve All Users:
* **Objective:** Display all records from the `users` table.
* **SQL Query:**
    ```sql
    SELECT * FROM users;
    ```
* **Expected Output:**
    ```
    user_id | username | email                | reg_date
    --------|----------|----------------------|----------
    1       | alice    | alice@example.com    | 2023-01-10
    2       | bob      | bob@example.com      | 2023-02-15
    3       | charlie  | charlie@example.com  | 2023-03-01
    4       | eve      | eve@example.com      | 2023-04-20
    ```
* **Explanation:** The `SELECT *` statement retrieves all columns, and `FROM users` specifies the table.

### 2. Find Users Registered After a Specific Date:
* **Objective:** List users who registered after March 1, 2023.
* **SQL Query:**
    ```sql
    SELECT user_id, username, reg_date FROM users WHERE reg_date > '2023-03-01';
    ```
* **Expected Output:**
    ```
    user_id | username | reg_date
    --------|----------|----------
    3       | charlie  | 2023-03-01
    4       | eve      | 2023-04-20
    ```
* **Explanation:** The `WHERE` clause filters records based on a condition.

### 3. Count Total Logins:
* **Objective:** Determine the total number of 'login' activities recorded.
* **SQL Query:**
    ```sql
    SELECT COUNT(*) FROM user_activity WHERE activity_type = 'login';
    ```
* **Expected Output:**
    ```
    COUNT(*)
    --------
    5
    ```
* **Explanation:** `COUNT(*)` is an aggregate function that returns the number of rows.

### 4. List All Activities for a Specific User:
* **Objective:** Retrieve all activities performed by 'alice'.
* **SQL Query:**
    ```sql
    SELECT ua.activity_type, ua.activity_date, ua.ip_address
    FROM user_activity ua
    JOIN users u ON ua.user_id = u.user_id
    WHERE u.username = 'alice';
    ```
* **Expected Output:**
    ```
    activity_type | activity_date       | ip_address
    --------------|---------------------|------------
    login         | 2023-05-01 08:00:00 | 192.168.1.10
    view_page     | 2023-05-01 08:05:00 | 192.168.1.10
    logout        | 2023-05-01 08:30:00 | 192.168.1.10
    login         | 2023-05-02 09:15:00 | 192.168.1.11
    ```
* **Explanation:** `JOIN` combines rows from two or more tables based on a related column. `ON` specifies the join 
condition.

### 5. Count Activities by Type:
* **Objective:** Count how many times each type of activity occurred.
* **SQL Query:**
    ```sql
    SELECT activity_type, COUNT(*) AS total_count
    FROM user_activity
    GROUP BY activity_type;
    ```
* **Expected Output:**
    ```
    activity_type | total_count
    --------------|------------
    login         | 5
    logout        | 3
    purchase      | 2
    view_page     | 7
    ```
* **Explanation:** `GROUP BY` groups rows that have the same values in specified columns into a summary row. 
`COUNT(*)` aggregates the count for each group.

## Conclusion and Future Enhancements

These examples illustrate fundamental SQL querying capabilities crucial for data extraction and basic analysis. 
Mastering these operations is key for anyone working with structured data, whether for business intelligence, 
reporting, or security investigations.

Future SQL examples could include:
* More complex `JOIN` scenarios (e.g., `LEFT JOIN`, `RIGHT JOIN`).
* Subqueries and Common Table Expressions (CTEs).
* Data modification (`INSERT`, `UPDATE`, `DELETE`).
* Indexing for performance optimization.
