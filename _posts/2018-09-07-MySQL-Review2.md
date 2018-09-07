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
