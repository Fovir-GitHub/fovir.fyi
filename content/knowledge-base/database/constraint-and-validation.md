---
# prettier-ignore
date: 2025-11-25
title: Constraint and Validation
description: Introduction of database constraint and validation.
weight: 11
---

## Integrity Constraints

Integrity constraints guard against accidental damage to the database by ensuring the authorized changes to the database do not result in a loss of data consistency.

They include

- Domain Constraint
- Referential Integrity
- Assertions
- Triggers

## Domain Constraints

They define valid values for attributes, including `string`, `character`, `integer`, `time`, `date`, `currency`, etc.

## Type of Constraints

| Constraints                                                                                      | Key                                            |
| ------------------------------------------------------------------------------------------------ | ---------------------------------------------- |
| **Entity Constraint** is given within one table.                                                 | `PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, `NULL` |
| **Referential Constraint** is used for referring other tables to enforce conditions on the data. | `FOREIGN KEY`                                  |
| **Semantic Constraint** which typically refer to data types.                                     | Data types                                     |

## Key Constraint

There are 5 types of key constraints in DBMS:

1. `NOT NULL`: Ensure the column is not a `NULL` value.
2. `UNIQUE`: Ensure values in the column are not duplicated.
3. `DEFAULT`: Provide a default value for a column.
4. `CHECK`: Check for the predefined conditions before inserting data into the table.
5. `PRIMARY KEY`: It uniquely identifies a row in a table.
6. `FOREIGN KEY`: Ensure referential integrity of the relationship.

### Use `CHECK`

```sql
CREATE TABLE my_table (
  id INT PRIMARY KEY,
  age INT CHECK (age >= 18)
);

INSERT INTO my_table (id, age) VALUES (1, 5);
```

The statement above will fail since the age inserted is less than $18$.

## Trigger

A trigger is a statement that is executed automatically by the system when modifying the database.

To design a trigger, two things should be specified:

1. Conditions under which the trigger is to be executed.
2. Actions to be taken when the trigger executes.

### Benefits of Trigger

1. Generating some derived column values automatically
2. Enforcing referential integrity
3. Event logging and storing information on table access
4. Auditing
5. Synchronous replication of tables
6. Imposing security authorizations
7. Preventing invalid transactions
