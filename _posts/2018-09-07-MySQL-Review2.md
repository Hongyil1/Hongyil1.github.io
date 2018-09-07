---
layout:     post
title:      MySQL Review 2
subtitle:   Knowledge and command in MySql
date:       2018-09-07
author:     Hongyi
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - MySQL
---

## Sorting data
### ORDER BY
When you use *SELECT statement* to query data from a table, the result set is not sorted in any orders. To sort the result set, you use the *ORDER BY* clause. The *ORDER BY* clause allows you to:
* Sort a result set by a single column or multiple columns.
* Sort a result set by different columns in ascending or descending order.

```
SELECT column1, column2, ...
FROM tbl
ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...
```
For example, if you want to sort the contacts by the last name in descending order and the first name in ascending order, you specify both DESC and ASC in the 
corresponding column as follows:

```
SELECT
  contactLastname,
  contactFirstname
FROM
  customers
ORDER BY
  contactLastname DESC,
  contactFirstname ASC;
```

**MySQL ORDER BY sort by an expression example**

The *ORDER BY* clause also allows you to sort the result set based on an expression.

The following query selects the order line items from the orderdetails table. It calculates the subtotal for each line item and sorts the result set based on the order number, order line number, and subtotal.
```
SELECT
  ordernumber,
  orderlinenumber,
  quantityOrdered * priceEach AS subtotal
FROM
  orderdetails
ORDER BY
  ordernumber,
  orderLineNumber,
  quantityOrdered * priceEach;
```

**ORDER BY with custom sort order**

The *ORDER BY* clause enables you to define your own custom sort order for the values in a column using the *FIELD()* function.

For example, if you want to sort the orders based on the following status by the following order:
* In Proces
* On Hold
* Cancelled
* Resolved
* Disputed
* Shipped

```
SELECT
  orderNumber, status
FROM
  orders
ORDER BY FIELD(status,
          "In Process",
          "On Hold",
          "Cancelled",
          "Resolved",
          "Disputed",
          "Shipped");
```

## Joining tables
### Alias
MySQL supports two kinds of aliases which are known as column alias and table alias.

**Alias for columns**
Sometimes the names of columns are so technical that make the query's output very difficult to understand. To give a column a descriptive name, you use a column alias.

```
SELECT
    [column_1 | expression] AS descriptive_name
FROM
    table_name;
```

To give a column an alias, you use the *AS* keyword followed by the alias. If the alias contains space, you must quote it as the following:

```
SELECT 
    [column_1 | expression] AS 'descriptive name'
FROM
    table_name;
```

For example, the following query selects first names and last names of employees and combines them to produce the full names. The **CONCAT_WS** function is used to concatenate first name and last name.

```
SELECT
    CONCAT_WS(', ', lastName, firstname)
FROM
    employees;
```

> The CONCAT and CONCAT_WS functions are used to combine strings.

```
SELECT CONCAT('AB', 'CD');
--------------------------
ABCD
```

> CONCAT_WS means concat with separator.

```
SELECT CONCAT_WS(',', '11', '22', '33');
----------------------------------------
11,22,33
```

The following statement selects the orders whose total amount are greater than 60000. It uses column aliases in GROUP BY and HAVING clauses.

```
SELECT
    orderNumber AS `Order no.`,
    SUM(priceEach * quantityOrdered) AS total
FROM
    orderdetails
GROUP BY
    `Order no.`
HAVING 
    total > 60000;
```

> It's ` instead of '.

> You cannot use a column alias in the WHEREclause. The reason is that when MySQL evaluates the WHERE clause, the values of columns specified in the SELECT clause may not be determined yet.

**Alias for tables**

You can use an alias to give a table a different name. You assign a table an alias by using the AS keyword as the following syntax:

```
table_name AS table_alias
```

You often use the table alias in the statement that contains **INNER JOIN, LEFT JOIN, self join** clauses, and in subsqueries.

```
SELECT 
    customerName,
    COUNT(o.orderNumber) total
FROM
    customers c
INNER JOIN orders o ON c.customerNumber = o.customerNumber
GROUP BY
    customerName
ORDER BY
    total DESC;
```

### JOIN
A relational database consists of multiple related tables linking together using common columns which are kown as **foreign key** columns. Because of this, data in each table is incomplete from the business perspective.

MySQL supports the following types of joins:
1. Cross join
2. Inner join
3. Left join
4. Right join

To make easy for understanding, we will use the t1 and t2 tables with the following structures:

```
CREATE TABLE t1 (
    id INT PRIMARY KEY,
    pattern VARCHAR(50) NOT NULL
);

CREATE TABLE t2(
    id VARCHAR(50) PRIMARY KEY,
    pattern VARCHAR(50) NOT NULL
);
```

Then we insert data into both t1 and t2 tables:

```
INSERT INTO t1(id, pattern)
VALUES
    (1, 'Divot'),
    (2, 'Brick'),
    (3, 'Grid');

INSERT INTO t2(id, pattern)
VALUES
    ('A', 'Brick'),
    ('B', 'Grid'),
    ('C', 'Diamond');
```

**CROSS JOIN**

The CROSS JOIN makes a Cartesian product(笛卡尔乘积) of rows from multiple tables. Suppose, you join t1 and t2 tables using the CROSS JOIN, the result set will include the combinations of rows from the t1 tables with the rows in t2 table.

```
SELECT
    t1.id, t2.id
FROM
    t1
CROSS JOIN t2;
```

| id    | id    |
|:------|:------|
| 1     | C     |
| 1     | B     |
| 1     | A     |
| 2     | C     |
| 2     | B     |
| 2     | A     |
| 3     | C     |
| 3     | B     |
| 3     | A     |

<img width="426" alt="cross join" src="https://user-images.githubusercontent.com/22671087/45215143-e2f5a280-b2df-11e8-9468-4b1cb51a8ef7.PNG">

**INNER JOIN**

An INNER JOIN requires rows in the two joined tables to have matching column values. The INNER JOIN creates the result set by combining column values of two joined tables based on the join-predicate. To join two tables, the INNER JOIN compares each row in the first table with each row in the second table to find pairs of rows that satisfy the join-predicate. Whenever the join-predicate is satisfied by matching non_NULL value, column values for each matched pair of rows of the two tables are included in the result set.

```
SELECT
    t1.id, t2.id
FROM
    t1
        INNER JOIN
    t2 ON t1.pattern = t2.pattern;
```

In this statement, the join-predicate is t1.pattern = t2.pattern. It means that rows in t1 and t2 tables must have the same value in the pattern column to be included in the result.

| id    | id    |
|:------|:------|
| 2     | A     |
| 3     | B     |

<img width="418" alt="inner join" src="https://user-images.githubusercontent.com/22671087/45215613-5b109800-b2e1-11e8-8733-a4f51a42bc0e.PNG">

**LEFT JOIN**

Similar to an INNER JOIN, a LEFT JOIN also requires a join-predicate. When joining two tables, the concepts of left table and right table are introduced. A LEFT JOIN returns all rows in the left table including rows that satisfy join-predicate and rows that do not. For the rows that do not match the join-predicate, NULLs appear in the columns of the right table in the result set.

```
SELECT
    t1.id, t2.id
FROM
    t1
        LEFT JOIN
    t2 ON t1.pattern = t2.pattern
ORDER BY t1.id;
```

| id    | id    |
|:------|:------|
| 1     | NULL  |
| 2     | A     |
| 3     | B     |

<img width="420" alt="left join" src="https://user-images.githubusercontent.com/22671087/45215929-47196600-b2e2-11e8-8845-d33260a5fc6a.PNG">

**RIGHT JOIN**

A RIGHT JOIN is similar to the LEFT JOIN except that the treatment of tables is reversed.

```
SELECT
    t1.id, t2.id
FROM
    t1
        RIGHT JOIN
    t2 ON t1.pattern = t2.pattern
ORDER BY
    t2.id;
```
| id    | id    |
|:------|:------|
| 2     | A     |
| 3     | B     |
| NULL  | C     |

<img width="417" alt="right join" src="https://user-images.githubusercontent.com/22671087/45216108-cc9d1600-b2e2-11e8-9611-445a514e6e65.PNG">










