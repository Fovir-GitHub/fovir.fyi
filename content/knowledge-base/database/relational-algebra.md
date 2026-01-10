---
# prettier-ignore
date: 2025-12-02
title: Relational Algebra
description: Note of relational algebra.
weight: 13
---

## Introduction

Relational algebra is a procedural query language used to query and manipulate data in relational databases.

It provides a foundation for SQL, and defines operations on relations (or tables) to produce new relations.

The key features are:

- Operates on one or more relations.
- Outputs a new relation.
- Uses a mathematical approach.

It is very important because it:

- Forms the theoretical foundation of relational databases.
- Helps in query optimization.
- Translates user-friendly SQL queries into executable instructions.
- Promotes a deeper understanding of database operations.

## Query Processing

Query processing steps include:

1. Parsing and translation
2. Optimization
3. Evaluation

## Basic Relational Algebra Operations

| Operation           | Symbol   | Example                                                    |
| ------------------- | -------- | ---------------------------------------------------------- |
| `SELECT`            | $\sigma$ | $\sigma$ Status = "Active"(Customer)                       |
| `PROJECTION`        | $\pi$    | $\Pi$ CustomerName, Status (Customer)                      |
| `RENAME`            | $\rho$   | $\rho$ \${new_name} / \${old_name}                         |
| `UNION`             | $\cup$   | $A \cup B$ gives all tuples in table $A$ and $B$.          |
| `INTERSECTION`      | $\cap$   | $A \cap B$ gives all tuples both in $A$ and $B$.           |
| `DIFFERENCE`        | $-$      | $A - B$ gives tuples in $A$ but not in $B$.                |
| `CARTESIAN PRODUCT` | $\times$ | $A \times B$ gives combinations of columns in $A$ and $B$. |
| `JOIN`              | $\Join$  | None                                                       |

## Modification of Database

Operations of modifying databases:

- **Deletion**
- **Insertion**
- **Updating**

These operations are expressed using the assignment operator $\gets$.

### `Deletion`

$$
r \gets r - E
$$

Example:

$$
\text{Customer} \gets \text{Customer} - (\sigma \; \text{Status = `Active'(Customer)})
$$

### `Insertion`

$$
r \gets r \cup E
$$

Example:

$$
\text{Customer} \gets \text{Customer} \cup \{1, `\text{Name}', `\text{Active}'\}
$$

### `Updating`

Updating can be expressed by a sequence of deletion and insertion operations.
