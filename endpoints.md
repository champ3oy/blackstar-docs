# Endpoints

Get all our `endpoints` and `schema` data on our [Swagger UI](https://api.uatdev.blackstargroup.ai/swagger-ui/index.html)

### Note

1. Endpoints with `/public` path are public and do not require authentication with `access token`.
2. All other endpoints require authentication with `access token`.

### Authentication

Pass access token to the Header of the request

```json
"headers": {
    "Authorization": "Bearer <ACCESS_TOKEN>"
}
```
