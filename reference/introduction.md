---
title: Introduction
slug: introduction
category:
  uri: /branches/1.0/categories/reference/SeaDB%20API
position: 0
content:
  excerpt: >-
    This is the reference for the SeaDB API. On this page you will find
    everything you need to use the SeaDB API.
---

This is the reference for the SeaDB API.

SeaDB provides a REST-style HTTP API for querying data with SQL and managing bases, tables, columns, indexes and users. Requests use JSON, and responses use standard HTTP status codes. Some successful management operations return an empty body.

Use your own SeaDB server and account credentials. `https://seadb.example.com` is a placeholder in the examples. API paths begin with `/api/v1`; the health check is `/ping`.

Before calling an endpoint, see [Authentication](https://seadb-api.readme.io/reference/authentication-overview). Refer to [Terminology](https://seadb-api.readme.io/reference/terminology) for common terms and [Status Codes](https://seadb-api.readme.io/reference/status-codes) for error handling.
