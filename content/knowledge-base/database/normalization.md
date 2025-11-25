---
# prettier-ignore
date: 2025-11-25
title: Normalization
description: Introduction of normalization in database.
weight: 12
---

Normalization has the following functions:

- Evaluate and correct table structures to minimize **data redundancies**.
- Reduce **data anomalies**.
- Assign attributes to tables based on determination.

There are three normal forms:

1. First Normal Form (1NF)
2. Second Normal Form (2NF)
3. Third Normal Form (3NF)

| Normal Forms                      | Characteristic                                                 |
| --------------------------------- | -------------------------------------------------------------- |
| **First Normal Form (1NF)**       | Table format, no repeating groups, and primary key identified. |
| **Second Normal Form (2NF)**      | 1NF and no partial dependencies.                               |
| **Third Normal Form (3NF)**       | 2NF and no transitive dependencies.                            |
| **Boyce-Codd Normal Form (BCNF)** | Every determinant is a candidate key (special case of 3NF)     |
| **Fourth Normal Form (4NF)**      | 3NF and no independent multivalued dependencies.               |

## Reasons of Normalization

The database design must be efficient on performance, which should be free of update, insertion and deletion anomalies.

There are three anomalies to avoid:

| Anomaly                  | Effect                                                                             |
| ------------------------ | ---------------------------------------------------------------------------------- |
| **Insertion Anomaly**    | Adding new rows forces user to create duplicate data.                              |
| **Deletion Anomaly**     | Deleting rows may cause a loss of data that would be needed for other future rows. |
| **Modification Anomaly** | Change data in a row forces changes to other rows because of duplication.          |

## First Normal Form (1NF)

1. It should only have single (or atomic) valued attributes / columns (not a list).
2. All columns in a table should have unique names (No duplicate row).
3. Attributes domain should not be change.

## Second Normal Form (2NF)

1. It should be in the First Normal Form.
2. It should not have **partial dependencies**.
3. All columns depend on one primary key in one table (functional dependency).

Partial dependency means that, if there is a composite primary key in a table, and one column in this table only depends on one of the primary keys, it is called partial dependency.

For example, there is a table with a composite primary key `(id, name)`, but there is a column named `person` only depends on `id`, then the partial dependency occurs.

## Third Normal Form (3NF)

1. It is the first and second normal form.
2. It does not have **transitive dependency**.
3. One attribute depends on one attribute which is not primary key, can not take `NULL` values.

A **Transitive dependency** in a database is an indirect relationship between values in the same table that causes a functional dependency.

In another word, transitive dependency happens when a non-key attribute determines another non-key attribute.

For example, there are three columns having this relation:

```mermaid
graph LR
  A --> B --> C
```

Where `B` depends on `A`, and `C` depends on `B`, which is transitive dependency of `A`.

To fix this problem, these columns should be separated into two tables to meet the requirement of 3NF.
