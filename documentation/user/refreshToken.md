# Refresh Token

This endpoint allows users to refresh their access token, typically used to extend a session without requiring full re-authentication.

## Endpoint Details

- **URL**: `/api/public/user/refresh-token`
- **Method**: POST
- **Description**: Refreshes the user's access token

## Request

### Headers

- **Content-Type**: application/json
- **Accept**: application/json

### Request Body

The request body should be a JSON object. While the exact structure is not provided, it's likely to include the current refresh token:

```json
{
  "refreshToken": "string"
}
```

## Response

### Success Response

- **Code**: 200 OK
- **Content-Type**: application/json

The response body is likely to contain a new access token and possibly a new refresh token:

```json
{
  "accessToken": "string",
  "refreshToken": "string",
  "expiresIn": 3600
}
```

## Example Usage

### cURL

```bash
curl -X POST "https://api.example.com/api/public/user/refresh-token" \
     -H "Content-Type: application/json" \
     -H "Accept: application/json" \
     -d '{
           "refreshToken": "your_current_refresh_token"
         }'
```

### JavaScript (Axios)

```javascript
const axios = require("axios");

const url = "https://api.example.com/api/public/user/refresh-token";
const data = {
  refreshToken: "your_current_refresh_token",
};

axios
  .post(url, data, {
    headers: {
      "Content-Type": "application/json",
      Accept: "application/json",
    },
  })
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

## Notes

1. This endpoint is part of the public API, as indicated by the `/public/` in the URL path. However, it still requires a valid refresh token to function.

2. The primary purpose of this endpoint is to allow users to obtain a new access token without having to re-enter their credentials.

3. Refresh tokens are typically long-lived compared to access tokens. Ensure your application securely stores and manages refresh tokens.

4. If the refresh token is expired or invalid, this endpoint should return an error, and the user may need to re-authenticate fully.

5. Implement proper error handling for cases such as invalid tokens, network issues, or server errors.

6. Consider implementing rate limiting on this endpoint to prevent abuse.

7. After receiving a new access token, update it in your application's storage and use it for subsequent API requests.

8. The new access token will have its own expiration time, which may be returned in the `expiresIn` field (in seconds).

9. Some implementations might also issue a new refresh token with each refresh. If so, make sure to update both tokens in your application.

10. Be aware of the security implications of refresh tokens. If a refresh token is compromised, an attacker could potentially maintain access to the account for an extended period.
