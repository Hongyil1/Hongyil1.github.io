---
layout:     post
title:      MySQL Review 3
subtitle:   Knowledge and command in MySql
date:       2018-09-08
author:     Hongyi
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - MySQL
---

# MySQL constraints
### Priamary key constraint
A primary key is a column or a set of columns that uniquely identifies each row in the table. You must follow the rules below when you define a primary key for a table:
* A primary key must contain unique values. If the primary key consists of multiple columns, the combination of values in these columns must be unique.
* A primary key column cannot contain NULL values. It means that you have to declare the primary key column with the NOT NULL  attribute. If you don’t, MySQL will force the primary key column as NOT NULL  implicitly.
* A table has only one primary key.

A primary key column often has the AUTO_INCREMENT attribute that generates a unique sequence for the key automatically. The primary key of the next row is greater than the previous one.

**PRIMARY KEY vs. UNIQUE KEY vs. KEY**

A *KEY* is a synonym for INDEX. You use the KEY when you want to create an index for a column or a set of columns that is not the part of a primary key or unique key.

A *UNIQUE* index creates a constraint for a column whose values must be unique. Unlike the PRIMARY index, MySQL allows NULL values in the UNIQUE index. A table can also have multiple UNIQUE indexes.

### Foreign key
A foreign key is a field in a table that matches another field of another table. A foreign key places constraints on data in the related tables, which enables MySQL to maintain referential integrity.

A foreign key can be a column or a set of columns. The columns in the child table often refer to the primary key columns in the parent table. A table may have more than one foreign key, and each foreign key in the child table may refer to a different parent table.

Sometimes, the child and parent tables are the same. The foreign key refers back to the primary key of the table e.g., the following employees table.

# Database schema 
## Entity
![crows-foot-notation-entity](https://user-images.githubusercontent.com/22671087/45251124-40432f80-b384-11e8-8593-5d4985b3bffd.png)
## Attribute
![crows-foot-notation-attributes](https://user-images.githubusercontent.com/22671087/45251125-40432f80-b384-11e8-89b2-27ca3d6d140c.png)
## Relationships
### Zero or Many
![crows-foot-notation-zero-or-many](https://user-images.githubusercontent.com/22671087/45251127-42a58980-b384-11e8-938c-f8d4edd08bfb.png)
### One or Many
![crows-foot-notation-one-or-many](https://user-images.githubusercontent.com/22671087/45251128-433e2000-b384-11e8-8617-8cb46a62aca9.png)
### One and only one
![crows-foot-notation-one](https://user-images.githubusercontent.com/22671087/45251129-433e2000-b384-11e8-8da5-3a9b2c9c4058.png)
### Zero or One
![crows-foot-notation-one-or-zero](https://user-images.githubusercontent.com/22671087/45251130-433e2000-b384-11e8-9c63-35233adaddaf.png)









