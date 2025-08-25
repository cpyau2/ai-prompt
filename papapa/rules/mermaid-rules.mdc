---
description: Mermaid ER Diagram Rules
alwaysApply: true
globs: ["**/*.mmd", "**/*.md"]
---

# Mermaid ER Diagram Rules

**Scope**: Entity-Relationship (ER) diagrams only
**Applies to**: Inline diagrams and `.mmd` files

## Naming Conventions

**Table Names**: Always use singular form
**Table and Column Names**: Always use `snake_case`

```mermaid
erDiagram
    user_account {
        user_id bigint "NN, PK"
        email_address varchar(255) "NN, UK"
        created_at timestamp "NN"
    }

    user_profile {
        profile_id bigint "NN, PK"
        user_id bigint "NN, FK"
        display_name varchar(100)
        bio_text varchar(500)
    }
```

## Column Nullability

**Not Null**: Append `"NN"` (with double quotes) to column description
**Nullable**: No suffix needed

```mermaid
erDiagram
    product {
        product_id bigint "NN, PK"
        product_name varchar(100) "NN"
        description varchar(500)
        price numeric(10-2) "NN"
        is_active boolean "NN, {true, false}"
    }
```

## Data Types

**Varchar**: Use `varchar(<number>)` for known length, `varchar(0)` for unknown
**Numeric**: Use `numeric` instead of `decimal` for numeric data types
**Precision/Scale**: Use `numeric(10-2)` format (hyphen) instead of `numeric(10,2)` (comma) to avoid Mermaid syntax issues
**Primary Keys**: Use `bigint` instead of `int` for auto-incrementing surrogate keys, append "PK" to column description
**Foreign Keys**: Append "FK" to column description
**Unique Constraints**: Append "UK" to column description
**Avoid**: `string`, `array`, `JSON` data types

```mermaid
erDiagram
    order {
        order_id bigint "NN, PK"
        customer_name varchar(100) "NN"
        shipping_address varchar(0)
        order_status varchar(20) "NN, {pending, processing, shipped, delivered}"
    }
```

## Column Constraints

**Enum Values**: Include allowed values in description with `{value1, value2}`
**Multiple Descriptions**: Separate with commas

```mermaid
erDiagram
    user {
        user_id bigint "NN, PK"
        status varchar(20) "NN, {active, inactive, suspended}"
        role_type varchar(15) "NN, {admin, user, moderator}"
        email_verified boolean "NN, {true, false}"
    }
```

## Best Practices

- **Ensure 100% valid Mermaid syntax** for ER diagram preview
- **Avoid SQL keywords** for table/column names
- **Use multiple tables** instead of arrays/JSON for complex relationships
- **Separate multiple constraints** with commas: `"NN, {active, inactive}"`
