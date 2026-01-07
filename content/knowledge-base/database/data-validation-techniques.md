---
# prettier-ignore
date: 2026-01-07
title: Data Validation Techniques
description: Note of data validation techniques.
weight: 14
---

## Introduction

Data validation ensures data entered into a database is accurate, complete, and reliable. It helps to prevent incorrect, inconsistent, or duplicated data.

Data validation is essential for maintaining data integrity in SQL databases.

## Importance

- Reduce data entry and processing errors.
- Ensure consistency across datasets and systems.
- Enhances accuracy of reports and analytics.
- Enforces business automatically.

## Types

- **Format Validation:** Check pattern.
- **Range Validation:** Ensure values within limits.
- **Presence Validation:** Requires mandatory fields.
- **Referential Validation:** Maintains valid relationships between tables.

## Key Constraint

### `UNIQUE`

```sql
CREATE TABLE tb (
  id INT UNIQUE,
  name VARCHAR(50) NOT NULL
);
```

### `DEFAULT`

```sql
CREATE TABLE tb (
  id INT NOT NULL,
  name VARCHAR(50) NOT NULL
);
```

### `CHECK`

```sql
CREATE TABLE tb (
  id INT PRIMARY KEY,
  name VARCHAR(50) NOT NULL,
  age INT CHECK (age >= 18)
);
```

### Triggers

Example:

```sql
CREATE TRIGGER trigger_name
AFTER INSERT ON tb1
FOR EACH ROW
UPDATE tb
SET col1 = col1 + NEW.col2;
```

## Summary

- Constraints, triggers, and procedures can be combined for robust validation.
- Always validate at the database level.
- Use staging tables for import validation.
- Regularly audit and document validation rules.
- Good validation = clean, trustworthy data.
