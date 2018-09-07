---
layout:     post
title:      MySQL Review 1
subtitle:   Knowledge and command in MySql
date:       2018-09-06
author:     Hongyi
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - MySQL
---

# Relational Database vs Non-relational Database
**SQL database** uses structured query language (SQL) for defining and manipulating data. SQL requires that you use predefined schemas to determine the structure of your data before you work with it. All of your data must follow the same structure. Its advantages are that itis safer and great for complex queries. The downsides are that it lacks of the flexibiltiy and the data structure is fixed.

**NoSQL database** has dynamic schema for unstructured data, and data is stored in many ways. The data is stored in many ways: column-oriented, document-oriented, graph-based or organized as KeyValue store. The flexibility means that: 1. You don't need to define the data structure before you create the doucments. 2. The structure of documents can be different.

### MySQL vs MongoDB
The following are some **MySQL** benefits and strengths:
- Open source, it's free.
- MYSQL is available for all major platforms: Linux, Windows, Mac etc. 
- MYSQL can be connected to many programing languages like Python, PHP, Java, Node.js and so on.
- The MYSQL database can be replicated across multiple nodes. It can balance the workload.

The following are some **MongoDB** benefits and strengths:
- Open source, it's free.
- It's flexible to change the data structure.
- Its horizontal scalability is able to reduece the workload.
- It's high-performing for simple queries.

# Basic MySQL Command
## MYSQL start
### MySQL Connection
```
sudo service mysql start
mysql -u root
```
### Create MySQL database
```
create database database_name;
```
### Delete database
```
drop database database_name;
```
### Choose database
```
show databases;
use database_name;
```
### Data Type
There are three main types in MySQL database: **Numeric** types, the **DATATIME, DATE and TIMESTAMP** types and **String** Types. 
#### Numeric

| Types         | Length in Bytes| Range                    |
| :-----------: |:--------------:| :-----------------------:|
| TINYINT       | 1              | (-128，127)              |
| SMALLINT      | 2              | (-32 768，32 767)        |
| MEDIUMINT     | 3              | (-8 388 608，8 388 607)  |
| INT/INTEGER   | 4              | (-2 147 483 648，2 147 483 647) |
| BIGINT        | 8              | (-9 233 372 036 854 775 808，9 223 372 036 854 775 807) |
| FLOAT         | 4              | (-3.402 823 466 E+38，-1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38) |
| DOUBLE        | 8              | (-1.797 693 134 862 315 7 E+308，-2.225 073 858 507 201 4 E-308)，0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) |
| DECIMAL       | DECIMAL(M,D):if M>D: M+2, else: D+2       | Depends on M, D |

#### DATATIME, DATE and TIMESTAMP

| Types         | Length in Bytes| Range                    | Format    |
| :-----------: |:--------------:| :-----------------------:| :--------:|
| DATE          | 3              | 1000-01-01/9999-12-31              | YYYY-MM-DD   |
| TIME          | 3              | '-838:59:59'/'838:59:59'        | HH:MM:SS   |
| YEAR          | 1              | 1901/2155              | YYYY   |
| DATETIME      | 8              | 1000-01-01 00:00:00/9999-12-31 23:59:59        | YYYY-MM-DD HH:MM:SS   |
| TIMESTAMP     | 4              | 1970-01-01 00:00:00/2038        | YYYYMMDD HHMMSS   |

#### String

| Types         | Range          |
| :-----------: |:--------------:|
| CHAR          | 0-255 (constant length)              | 
| VARCHAR          | 0-65535 (changeable length)             | 
| TINYBLOB         | 0-255 (binary string)              | 
| TINYTEXT      | 0-255              | 
| BLOB     | 0-65 535              |
| TEXT          | 0-65 535             | 
| MEDIUMBLOB          | 0-16 777 215              | 
| MEDIUMTEXT         | 0-16 777 215              | 
| LONGBLOB      | 0-4 294 967 295              | 
| LONGTEXT     | 0-4 294 967 295              |

### Create Table 
```
create table table_name (column_name column_type);
```
```
create table if not exists runoob_tbl(
    runoob_id INT UNSIGNED AUTO_INCREMENT,
    runoob_title VARCHAR(100) NOT NULL,
    runoob_author VARCHAR(40) NOT NULL,
    submission_date DATE,
    PRIMARY KEY (runoob_id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```
**NOT NULL** enforces the input to be not null. **AUTO_INCREMENT** is mainly used in Primary key.

### Delete table
```
DROP TABLE table_name;
```
### Insert data
```
INSERT INTO table_name (field1, field2, ...fieldN)
                        VALUES
                        (value1, value2,...valueN);
```
## MYSQL Query
The Sample Database comes from [MySQL Tutorial](http://www.mysqltutorial.org/mysql-sample-database.aspx).
MySQL Sample Database Schema shows below:
* **Customers**: stores customer's data
* **Products**: stores a list of scale model cars.
* **ProductLines**: stores a list of product line categories.
* **Orders:**: stores sales orders placed by customers.
* **OrderDetails**: stores sales order line items for each sales order.
* **Payments**: stores payments made by customers based on their account.
* **Employees**: stores all employee information as well as the organization structure such as who reports to whom.
* **Offices**: stores sales office data.

<p align="center">
<img width="600" alt="mysql-sample" src="https://user-images.githubusercontent.com/22671087/45188811-5c0ddf00-b279-11e8-93c7-290862425507.PNG"></p>

### Select
```
SELECT [DISTINCT]
    column_1, column_2, ...
FROM
    table_1
[INNER | LEFT | RIGHT] JOIN table_2 ON conditions
WHERE
    conditions
GROUP BY column_1
HAVING group_conditions
ORDER BY column_1
LIMIT offset, length;
```
* **DISTINCT** is used to eliminate duplicate rows in a result set.
* **FROM** specifies the table or view where you want to query the data.
* **JOIN** gets related data from other tables based on specific join conditions.
* **WHERE** clause filters row in the result set.
* **GROUP BY** groups a set of rows into groups and applies aggregate functions on each group.
* **HAVING** filters group based on groups defined by GROUP BY clause.
* **ORDER BY** specifies a list of columns for sorting.
* **LIMIT** constrains the number of returned rows.

### Where
```
SELECT
    select_list
FROM
    table_name
WHERE
    search_condition_1 AND/OR
    search_condition_2;
```
The *search_condition* is a combination of one or more predicates using the logical operator **AND, OR and NOT**. In SQL, a predicate is an expression that evaluates to true, false, or unknown.

| Operator  | Description              |
|:----------|:-------------------------|
| =         | Equal to.                |
| <> or !=  | Not equal to.            |
| <         | Less than                |
| >         | Greater than             |
| <=        | Less than or equal to    | 
| >=        | Greater than or equal to |

### AND
The *AND* operator is a logical operator that combines two or more **Boolean** expressions and returns true only if both expressions evaluate to true.
```
WHERE boolean_expression_1 AND boolean_expression_2
```
|          | **TRUE**  | **FALSE** | **NULL**  |
|:--------:|:---------:|:---------:|:---------:|
| **TRUE** | TRUE      | FALSE     | NULL      |
| **FALSE**| FALSE     | FALSE     | FALSE     |
| **NULL** | NULL      | FALSE     | NULL      |

The *AND* operator is often used in the **WHERE** clause of the **SELECT, UPDATE, DELETE** statement to form Boolean expressions. The *AND* operator is also used in join conditions of the **INNER JOIN** and **LEFT JOIN** clauses.

When evaluating an expression that has the *AND* operator, MySQL evaluates the remaining parts of the expression until it can determoine the result. This function is called short-circuit evaluation.

```
SELECT 1 = 0 AND 1 / 0;
-------------------------
0
```
MySQL only evaluates the first part *1 = 0* of the expression *1 = 0 AND 1 / 0*. Because the expression *1 = 0* return false, MySQL can conclude the result of the whole expression, which is false. MySQL then does not evaluate the remaining part of the expression.

### OR
MySQL *OR* operator combines two Boolean expressions and returns true when either condition is true.

```
boolean_expression_1 OR boolean_expression_2
```
|          | **TRUE**  | **FALSE** | **NULL**  |
|:--------:|:---------:|:---------:|:---------:|
| **TRUE** | TRUE      | TRUE      | TRUE      |
| **FALSE**| TRUE      | FALSE     | NULL      |
| **NULL** | TRUE      | NULL      | NULL      |

```
SELECT 1 = 1 OR 1 / 0;
-----------------------------
1
```
The MySQL also uses short-circuit evaluation for the *OR* operator. The result is 1 because the expression 1 = 1 return true, MySQL does not evaluate the 1 / 0.

** Operator precedence **
MySQL evaluates the *OR* operators **after** the *AND* operators.

```
SELECT true OR false AND false;
-------------------------------
1
```
How it works:
1. First, MySQL evaluates false AND false, return false.
2. Second, MySQL evaluate true OR false, return true.

To change the order of evaluation, you use **parentheses**.
```
SELECT (true OR false) AND false;
----------------------------------
0
```

The following statement returns the customers who locate in the USA or France and have credit limit greater than 100000.
```
SELECT
    customername, counrty, creditLimit
FROM
    customers
WHERE
    (counrty = "USA" OR country = "France")
    AND creditlimit > 100000;
```
If you do not use the **parentheses**, the query will return the customers who locate in the USA or the customers who locate in France with the credit limit greater than 10000.

### IN
The *IN* operator allows you to determine if a specified value mateches any one of a list or a subquery.
```
SELECT
    column1, column2, ...
FROM
    table_name
WHERE
    (expr|column_1) IN ("value1", 'value2', ...)
```
* You can use a column or an expression (expr) with the *IN* operator in the WHERE clause.
* The values in the list must be seperated by a comma(,).
* The *IN* operator can also be used in the WHERE clause of other statments such as **INSERT, UPDATE, DELETE**, etc.

The *IN* operator returns 1 if the value of the column_1 or the result of the expr is equal to any value in the list, otherwise, it returns 0.

When the values in the list are all **constants**:
* First, MySQL evaluates the values based on the type of the column_1 or result of the expr.
* Second, MySQL sorts the values.
* Third, MySQL searchs for the values using **binary search** algorithm. Therefore, a query that uses the *IN* operator with a list of constants will perform very fast.

> Note that if the expr or any value in the list is **NULL**, the IN operator returns NULL.

**MySQL IN with subquery**
The *IN* operator is often used with a **subquery**. Instead of providing a list of constant values, the subquery probides the list of values. Let's take a look at the orders and orderDetailes tables:

<p align="center">
<img width="450" alt="in-subquery" src="https://user-images.githubusercontent.com/22671087/45194234-8372a500-b295-11e8-8e7b-57996423abeb.PNG"></p>

For example, if you want to find orders whose total amounts are greater than 60000, you use the *In* operator as the following query:
```
SELECT
    orderNumber, customerNumber, status, shippedDate
FROM
    orders
WHERE
    orderNumber IN (SELECT
        orderNumber
    FROM
        orderDetails
    GROUP BY orderNumber
    HAVING SUM(quantityOrdered * priceEach) > 60000);
```

### BETWEEN
The *BETWEEN* operator allows you to specify a range to test. You often use the *BETWEEN* operator in the **WHERE** clause of the SELECT, UPDATE and DELETE statements.

```
expr [NOT] BETWEEN begin_expr AND end_expr;
```
All three expressions: expr, begin_expr, and end_expr must have the same **data type**.

The *BETWEEN* operator returns true if the value of the expr is greater than or equal to the value of begin_expr and less than or equal to the value of the end_expr otherwise it returns zero. If any expression is NULL, the *BETWEEN* operator returns a NULL value.

**MySQL BETWEEN with dates example**
When you use the *BETWEEN* operator with date values, to get the best result, you should use the type cast to explicitly convert the type of column or expression to the DATE type.

For example, to get the orders whose required dates are from 01/01/2003 to 01/31/2003, you use the following query:
```
SELECT
    orderNumber,
    requiredDate,
    status
FROM
    orders
WHERE
    requiredate BETWEEN
    CAST('2003-01-01' AS DATE) AND
    CAST('2003-03-31' AS DATE);
```

### LIKE
The *LIKE* operator is commonly used to select data based on patterns. Using the *LIKE* operator in the right way is essential to increase the query performance.

The MySQL provides two wildcard characters for using with the *LIKE* operator, the percentage% and underscore_.
* The percentage(%) wildcard allows you to macth any string of zero or more characters.
* The underscore(\_) wildcard allows you to match any single character.

**MySQL LIKE with percentage(%) wildcard**
Suppose you want to search for employee whose first name starts with character a, you can use the percentage wildecard(%) at the end of the pattern as follows:

```
SELECT
    employeeNumber,
    lastName,
    firstName
FROM
    employees
WHERE
    firstName LIKE 'a%';
```

To search for employee whose last name ends with on e.g., Patterson, Thompson, you can use the % wildcard at the beginning of the pattern as the following query:

```
SELECT
    employeeNumber,
    lastName,
    firstName
FROM
    employees
WHERE
    lastName LIKE '%on';
```

If you know the searched string is embedded inside in the column, you can use the percentage(%) wildcard at the beginning and the end of the pattern.

```
SELECT
    employeeNumber,
    lastName,
    firstName
FROM
    employees
WHERE
    lastname LIKE '%on%';
```

**MySQL LIKE with underscore(\_) wildcard**
To find employee whose first name starts with T, end with m and contains any single character between e.g., Tom, Tim, you use the underscore wildcard to construct the pattern as follows:

```
SELECT
    employeeNumber,
    lastName,
    firstName
FROM
    employees
WHERE
    firstname LIKE 'T_m';
```

> Note that the pattern is **not case sensitive** with the *LIKE* operator, therefore, the b% and B% patterns produce the same result.

**MySQL LIKE with ESCAPE clause**
Sometimes the pattern, which you want to match, contains wildcard character e.g.,10%, \_20, etc. In these cases, you can use the *ESCAPE* clause to specify the escape character so that MySQL interprets the wildcard character as a literal character. If you don't specify the escape character explicitly, the backslash character \ is the default escape character.

For example, if you want to find product whose product code contains string \_20, you can use the pattern %\\_20% as the following query:

```
SELECT
    productCode,
    productName
FROM
    products
WHERE
    productCode LIKE '%\\_20';
```

Or you can specify a different escape character e.g., $ by using the ESCAPE clause:

```
SELECT
    productCode,
    ProductName
FROM
    products
WHERE
    productCode LIKE '%$_20%' ESCAPE '$';
```

### LIMIT
The *LIMIT* clause is used in the SELECT statement to constrain the number of rows in a result set. The *LIMIT* clause accepts one or two arguments. The values of both arguments must be zero or positive integers.

```
SELECT
    column1, column2, ...
FROM
    table
LIMIT offset , count;
```

Let's examine the *LIMIT* clause parameters:
* The offset specifies the offset of the first row to return. The offset of the first row is 0, not 1.
* The *count* specifies the maximum number of rows to return.

<p align="center">
<img width="300" alt="offset" src="https://user-images.githubusercontent.com/22671087/45200849-10c5f180-b2b6-11e8-9d4e-2f03b0f4799f.PNG"> </P>

**Using LIMIT to get the highest and lowest values**
The *LIMIT* clause often used with the *ORDER BY* claus.

For example, to select top five customers who have the highest/lowest credit limit, you use the following query:

```
SELECT
    customernumber,
    customername,
    creditlimit
FROM
    customers
ORDER BY
    creditlimit DESC/ASC
LIMIT 5;
```

**Using LIMIT to get the nth highest value**
1. First, you sort the result set in descending order.
2. Second, you use *LIMIT* clause to get the nth most expensive product.

```
SELECT
    column1, column2, ...
FROM
    table
ORDER BY column1 DESC
LIMIT n-1, count;
```
For example, if you want to get the third most expernsive product:
```
SELECT
    productname, buyprice
FROM
    products
ORDER BY
    buyprice DESC
LIMIT 2, 1;
```
### IS NULL
To test whether a value is NULL or not, you use the *IS NULL* operator. If the value is NULL, the expression returns true. Otherwise, it returns false.
```
value IS NULL
```


