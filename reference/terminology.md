---
title: Terminology
slug: terminology
category:
  uri: /branches/1.0/categories/reference/SeaDB%20API
position: 1
content:
  excerpt: Bases, tables, columns, credentials and other terms used in SeaDB.
---

## Users and credentials

| Term | Meaning |
| --- | --- |
| `username` | Unique SeaDB account identifier. |
| `roles` | `default_role` for ordinary users; `admin` for administrators. |
| Base owner | The account that owns a base. Administrators can access all bases. |
| API key | An account credential used with the `ApiKey` authorization scheme. |
| Base JWT | A base-scoped credential used with the `Bearer` scheme. |

## Bases and tables

- **Base**: a database containing tables, columns, indexes and rows.
- **`base_id`**: the base UUID or its assigned name in API paths. Creation requires a lowercase UUID.
- **Base name**: an optional, globally unique alias.
- **`table_id`** / **`table_name`**: the internal table identifier and its name. Endpoints accepting either require at least one.
- **`_pk`**: the built-in auto-increment primary key. Row APIs use `pk` or `pks` for these unsigned integer values.

## Columns and values

- **Column key** (`key` / `column_key`): the internal column identifier.
- **Column name** (`name` / `column_name`): used in SQL and as row API object keys.
- **Column data** (`column_data` / `data`): type-specific settings, such as select options, compression and defaults.
- **Select option**: an `id` and display `name`. Row APIs accept option names.

Supported column types:

| Type | Value / metadata |
| --- | --- |
| `text` | String. |
| `int64` | Integer. |
| `float32`, `float64` | Floating-point number. |
| `bool` | Boolean. |
| `datetime` | Date/time string, e.g. `2019-11-05T00:00:00+08:00`. |
| `single-select` | A single option selected from predefined options. |
| `multiple-select` | An array of options selected from predefined options. |
| `list` | Array of elements of the same type. Element type is set in the `list_type` field of column data object. |

## Indexes

- **Index**: an ordered set of indexed columns, identified by `index_id`.
- **Unique index**: requires unique values or combinations, including null values.
- **Index task**: asynchronous index creation, identified by `task_id`.

## Templates

A **template** is a table whose column and index definitions can be shared by other tables. A table that uses a template table takes its column and index definitions from it, so a change to the template table applies to all the tables that use it.

Every user can define their own template tables. Templates created by different users are isolated.
