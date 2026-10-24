---
title: Status Codes
slug: status-codes
category:
  uri: /branches/1.0/categories/reference/SeaDB%20API
position: 3
content:
  excerpt: HTTP success codes, application errors and response-body handling.
---

SeaDB uses HTTP status codes to indicate success or failure.

| HTTP status | Meaning in SeaDB |
| --- | --- |
| **200 OK** | Request processed or background work scheduled. |
| **400 Bad Request** | Invalid parameters or SQL, unsupported operation, or canceled request. |
| **403 Forbidden** | Invalid credentials, unsupported authentication method, or insufficient permissions. |
| **404 Not Found** | Resource or endpoint not found. |
| **405 Method Not Allowed** | HTTP method not supported. |
| **408 Request Timeout** | Request exceeded its timeout. |
| **409 Conflict** | A query or row operation conflicts with another transaction. |
| **413 Content Too Large** | Batch row-operation limit exceeded. |
| **429 Too Many Requests** | Server request-rate limit exceeded. |
| **500 Internal Server Error** | Server or storage operation failed. |
| **503 Service Unavailable** | Server shutting down or base unavailable on this cluster node. |

Authentication failures return **403**, rather than 401. Resource and validation errors may vary by endpoint; see its response definitions.

## Error bodies

Application errors normally include `error_message`:

```json
{"error_message":"permission denied"}
```

Insert errors may include `inserted_row_count` and `pks` for rows already written. Check these before retrying. Router, rate-limit and shutdown errors may be plain text.

## Successful responses

Success bodies may be JSON or empty, as specified by each endpoint. Row-count recalculation returns before completion; asynchronous index creation returns a task ID for status polling.
