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

