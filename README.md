# Filter-a-SQL-query-Activity
Apply basic filters to SQL queries to retrieve information from a database. You’ll use SQL to get specific information about employees, their machines, and the departments they’re in. You’ll be using the MariaDB shell to run SQL queries.

## Table of contents

1. [Scenario](#scenario)
2. [List all organization machines](#list)
3. [Retrieve a list of the machines with OS 2](#retrieve)
4. [List employees in specific departments](#specific)
5. [Identify employee machines](#identify)
6. [Conclusion](#conclusion)

## Scenario <a name="scenario">
In this scenario, you need to get specific information about employees, their machines, and the departments they’re in. Your team needs this data to perform various tasks, such as running updates, posting a privacy notice in certain departments, and sending an alert to an employee with an issue on a machine.

You are responsible for finding the required information by querying a database. You’ll add filters to your queries to locate the information more quickly.

Here’s how you’ll do this task: First, you’ll list all organization machines and their operating systems. Second, you’ll list all machines with the operating system OS 2. Third, you’ll list all the employees in the Finance and Sales departments. Fourth, you’ll obtain information about machines.

You’re ready to add filters to SQL queries.

### Note:  
This text is for taking notes. It is part of a pre-made lab, so follow along and understand the process.

## List all organization machines <a name="list">
We need to get a list of all organization machines and their operating systems. The data is contained in the `machines` table. You’ll need to use the `SELECT` keyword to return specific columns.

- Run a SQL query to retrieve only the `device_id` and `operating_system` columns from the `machines` table.
`SELECT device_id, operating_system FROM machines;`

How many rows were returned from the machines table? (You can view the number of rows at the bottom of the output.

    +--------------+------------------+
    | device_id    | operating_system |
    +--------------+------------------+
    | a184b775c707 | OS 1             |
    | a192b174c940 | OS 2             |
    | a305b818c708 | OS 3             |
    | a317b635c465 | OS 1             |
    | a320b137c219 | OS 2             |
    | a398b471c573 | OS 3             |
    | a667b270c984 | OS 1             |
    | a821b452c176 | OS 2             |
    | a998b568c863 | OS 3             |
    | b157c491d493 | OS 2             |
    | b239c825d303 | OS 1             |
    | b264c773d977 | OS 2             |
    | ....         |                  |
    +--------------+------------------+
    200 rows in set (0.001 sec)

- 200

## Retrieve a list of the machines with OS 2 <a name="retrieve">
We need to obtain a list of all machines with the `'OS 2'` operating system because these machines need an update. To get this information, you’ll run your first SQL query with a filter.

- Select all the records from the `machines` table with a value of `'OS 2'` in the `operating_system` column.
`SELECT device_id, operating_system FROM machines WHERE operating_system = 'OS 2';`

Note: The WHERE clause allows you to filter the results returned by a query by returning only the records that satisfy the condition.  

How many machines in the database use the OS 2 operating system?

    +--------------+------------------+
    | device_id    | operating_system |
    +--------------+------------------+
    | a184b775c707 | OS 1             |
    | a192b174c940 | OS 2             |
    | a305b818c708 | OS 3             |
    | a317b635c465 | OS 1             |
    | a320b137c219 | OS 2             |
    | a398b471c573 | OS 3             |
    | a667b270c984 | OS 1             |
    | a821b452c176 | OS 2             |
    | a998b568c863 | OS 3             |
    | b157c491d493 | OS 2             |
    | .....        |                  |
    +--------------+------------------+
    200 rows in set (0.000 sec)

    +--------------+------------------+
    | device_id    | operating_system |
    +--------------+------------------+
    | a192b174c940 | OS 2             |
    | a320b137c219 | OS 2             |
    | a821b452c176 | OS 2             |
    | b157c491d493 | OS 2             |
    | b264c773d977 | OS 2             |
    | b265c937d713 | OS 2             |
    | b806c503d354 | OS 2             |
    | b979c871d361 | OS 2             |
    | c150d982e144 | OS 2             |
    | c406d877e950 | OS 2             |
    | ....         |                  |
    +--------------+------------------+
    80 rows in set (0.023 sec)

- 80       

## List employees in specific departments <a name="specific">
We need to retrieve a list of all the employees in the Finance and Sales departments to obtain their office numbers. A notice about handling confidential financial information will be posted to these offices.

- Filter the rows returned from `department` column in the `employees` table to include only employees from the `'Finance'` department.
`SELECT *  FROM employees  WHERE department = 'Finance';`

What is the employee_id of the first row returned?
    
    +-------------+--------------+----------+------------+-------------+
    | employee_id | device_id    | username | department | office      |
    +-------------+--------------+----------+------------+-------------+
    |        1003 | d394e816f943 | sgilmore | Finance    | South-153   |
    |        1007 | h174i497j413 | wjaffrey | Finance    | North-406   |
    |        1008 | i858j583k571 | abernard | Finance    | South-170   |
    |        1010 | k242l212m542 | jlansky  | Finance    | South-109   |
    |        1015 | p611q262r945 | jsoto    | Finance    | North-271   |
    |        1017 | r550s824t230 | jclark   | Finance    | North-188   |
    |        1018 | s310t540u653 | abellmas | Finance    | North-403   |
    |        1022 | w237x430y567 | arusso   | Finance    | West-465    |
    |        1029 | d336e475f676 | ivelasco | Finance    | East-156    |
    |        1044 | s429t157u159 | tbarnes  | Finance    | West-415    |
    |....         |              |          |            |             |
    +-------------+--------------+----------+------------+-------------+
    38 rows in set (0.001 sec)

- 1003

- Modify the previous query so that it returns employees who are in the `'Sales'` department.
`SELECT *  FROM employees  WHERE department = 'Sales';`

How many employees work in the Sales department?

    +-------------+--------------+----------+------------+-------------+
    | employee_id | device_id    | username | department | office      |
    +-------------+--------------+----------+------------+-------------+
    |        1009 | NULL         | lrodriqu | Sales      | South-134   |
    |        1011 | l748m120n401 | drosas   | Sales      | South-292   |
    |        1024 | y976z753a267 | iuduike  | Sales      | South-215   |
    |        1025 | z381a365b233 | jhill    | Sales      | North-115   |
    |        1035 | j236k303l245 | bisles   | Sales      | South-171   |
    |        1039 | n253o917p623 | cjackson | Sales      | East-378    |
    |        1041 | p929q222r778 | cgriffin | Sales      | North-208   |
    |        1057 | f370g535h632 | mscott   | Sales      | South-270   |
    |        1063 | l686m140n569 | lpope    | Sales      | East-226    |
    |....         |              |          |            |             |
    +-------------+--------------+----------+------------+-------------+
    33 rows in set (0.001 sec)
- 33

## Identify employee machines <a name="identify">
Your team recently discovered that there are issues with machines in the South building. In this task, We need to obtain certain employee and computer information.

A machine in `'South-109'` has an issue. You need to determine which employee uses that computer so you can send them an alert.

- Write a query to identify which employee uses the office in `'South-109'`. (The data must be returned from the `office` column in the `employees` table.)
`SELECT *  FROM employees  WHERE office = 'South-109';`

Which of the following employees uses the computer with the issue?

    +-------------+--------------+----------+------------+-----------+
    | employee_id | device_id    | username | department | office    |
    +-------------+--------------+----------+------------+-----------+
    |        1010 | k242l212m542 | jlansky  | Finance    | South-109 |
    +-------------+--------------+----------+------------+-----------+
    1 row in set (0.001 sec)

- jlansky

Next, our team has determined that there is an issue with all the machines in the South building. Offices in the organization are named with the building name, a hyphen, and the office number in that building (for example, `'South-109'`).

- Modify the query you used in the previous step so that it returns information on all the employees in the `'South'` building. Use the `LIKE` operator with `%` in this query.
`SELECT *  FROM employees  WHERE office LIKE 'south%';`

Note: The `LIKE` keyword in SQL performs simple string matches. The matching pattern may include the wildcard `%` to represent a string of any length. This wildcard may be placed both before and after the targeted substring.

Which department does the first employee listed in the South building belong to?

    +-------------+--------------+----------+------------------------+-----------+
    | employee_id | device_id    | username | department             | office    |
    +-------------+--------------+----------+------------------------+-----------+
    |        1003 | d394e816f943 | sgilmore | Finance                | South-153 |
    |        1004 | e218f877g788 | eraab    | Human Resources        | South-127 |
    |        1005 | f551g340h864 | gesparza | Human Resources        | South-366 |
    |        1008 | i858j583k571 | abernard | Finance                | South-170 |
    |        1009 | NULL         | lrodriqu | Sales                  | South-134 |
    |        1010 | k242l212m542 | jlansky  | Finance                | South-109 |
    |        1011 | l748m120n401 | drosas   | Sales                  | South-292 |
    |        1013 | n205o559p243 | zbernal  | Information Technology | South-229 |
    |....         |              |          |                        |           |
    +-------------+--------------+----------+------------------------+-----------+
    41 rows in set (0.001 sec
- Finance

## Conclusion <a name="conclusion">
We now have practical experience in using SQL to

- apply the WHERE clause to filter what a SQL query returns and
- use the LIKE operator to filter for patterns.
