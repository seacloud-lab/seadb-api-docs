---
title: Authentication
slug: authentication-overview
category:
  uri: /branches/1.0/categories/reference/SeaDB%20API
position: 2
content:
  excerpt: Authenticate with a SeaDB account, an API key or a base-scoped JWT.
---

All APIs except `/ping` require an `Authorization` header. SeaDB supports three authentication methods:

| Scheme | Authorization header | Scope |
| --- | --- | --- |
| Basic | `Authorization: Basic <base64(username:password)>` | Account permissions. |
| ApiKey | `Authorization: ApiKey <encoded>` | The key owner's account permissions. |
| Bearer | `Authorization: Bearer <jwt_token>` | One base, with table and permission restrictions. |

Invalid credentials or insufficient permissions return **403**.

## Basic authentication

Basic authenticates with a username and password using standard Base64. With curl:

```shell
curl 'https://seadb.example.com/api/v1/users/bases' \
  --user "$SEADB_USERNAME:$SEADB_PASSWORD"
```

For integrations, use an API key instead of sending the account password on each request.

## API key authentication

Use Basic or ApiKey authentication to [create an API key](https://seadb-api.readme.io/reference/createapikey). Save the returned `encoded` value; the secret is only returned once.

`encoded` is unpadded URL-safe Base64 of `key_id:key`. Use it directly:

```shell
curl 'https://seadb.example.com/api/v1/users/bases' \
  --header "Authorization: ApiKey $SEADB_API_KEY"
```

Keys inherit the owner's permissions and remain valid until deleted or expired. See [List API keys](https://seadb-api.readme.io/reference/listapikeys) and [Delete API keys](https://seadb-api.readme.io/reference/deleteapikeys).

## Base JWT authentication

The base owner or an administrator can [obtain a base JWT](https://seadb-api.readme.io/reference/obtainjwttoken) using Basic or ApiKey authentication. Send the returned token as `Authorization: Bearer <jwt_token>`.

A JWT expires after **72 hours**. It specifies table-name patterns (`*` matches any characters) and permissions that apply to all matching tables:

| Permission | Allowed operations |
| --- | --- |
| `read` | Read/query matching tables. |
| `read-write` | Read and insert/update/delete rows in matching tables. |
| `all` | Data operations and table/column/option/index schema management. |

JWTs work on single-base SQL, row and schema APIs. Base management, users, credentials, index-task queries and administrative APIs require Basic or ApiKey. The `template` alias also requires Basic or ApiKey.

JWT access still depends on current account roles and base ownership. Obtain a new token after expiration or a base UUID change. There is no refresh or individual JWT-revocation API; deleting an API key does not revoke its issued JWTs.
