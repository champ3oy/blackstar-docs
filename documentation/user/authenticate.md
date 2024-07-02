# Authenticate User

This endpoint allows users to authenticate and log in to the system.

## Endpoint Details

- **URL**: `/api/public/user/authenticate`
- **Method**: POST
- **Description**: Authenticates a user and potentially bypasses OTP (One-Time Password) verification.

## Request

### Headers

- **Content-Type**: application/json
- **Accept**: application/json

### Request Body

```json
{
  "email": "string",
  "password": "string"
}
```

### Success Response

- **Code**: 200 OK
- **Content-Type**: application/json


### Body
```json
{
    "userId": "83d93f37-e143-4168-b833-8dbf238bc546",
    "email": "test@blackstargroup.ai",
    "firstName": "Jane",
    "lastName": "Doe",
    "pinEnabled": false,
    "accessToken": "eyJhbGciOiJSUzI1NiIs...",
    "refreshToken": "eyJhbGciOiJIUzI1NiC...",
    "clientId": "910c8839-XXXX-XXXX-XXXX-26eed7adc026",
    "clientCode": "JWXXXXXX",
    "hasPortfolios": true
}
```

## Example Usage

### cURL

```bash
curl -X POST "https://api.example.com/api/public/user/authenticate" \
     -H "Content-Type: application/json" \
     -H "Accept: application/json" \
     -d '{
           "email": "your_email",
           "password": "your_password"
         }'
```

### JavaScript (Axios)

```javascript
const axios = require("axios");

const url = "https://api.example.com/api/public/user/authenticate";
const data = {
  email: "your_email",
  password: "your_password",
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

1. This endpoint is part of the public API, as indicated by the `/public/` in the URL path. This suggests it doesn't require prior authentication to access.

2. The endpoint name suggests it might bypass OTP verification. This could be a feature for certain types of logins or under specific circumstances. Be aware of the security implications of bypassing additional verification steps.

3. Ensure that sensitive information like passwords is always sent over a secure, encrypted connection (HTTPS).

4. The response from this endpoint is likely to contain sensitive information such as authentication tokens. Handle this data securely in your application.

5. Implement proper error handling for cases such as invalid credentials, account lockouts, or server errors.

6. Consider implementing rate limiting on this endpoint to prevent brute force attacks.

7. If this endpoint indeed bypasses OTP, there should be clear documentation on when and why this bypass is used, and any additional security measures in place.

8. The exact authentication mechanism (e.g., JWT, session-based) is not specified and may vary based on the system's implementation.

9. After successful authentication, you may need to include the received authentication token in the headers of subsequent API requests to access protected endpoints.
