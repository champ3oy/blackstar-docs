# Check Status of Payment

Checks the status of a payment request.

## Overview

This API endpoint is used to check the status of a payment of a collection request.

### Endpoint

- **HTTP Method:** GET
- **Path:** `/api/client/{clientId}/collectionRequest/{collectionRequestId}/checkStatus`

#### Parameters

| Name                  | Type             | Description             |
| --------------------- | ---------------- | ----------------------- |
| `collectionRequestId` | `string` ($uuid) | Collection Request UUID |
| `clientId`            | `string` ($uuid) | Client UUID             |

#### Request Body

This endpoint does not require a request body.

#### Example Request

##### cURL

```bash
curl -X GET "https://api.example.com/api/client/{clientId}/collectionRequest/{collectionRequestId}/checkStatus" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

##### JavaScript (axios)

```javascript
const axios = require("axios");

axios
  .get(
    "https://api.example.com/api/client/{clientId}/collectionRequest/{collectionRequestId}/checkStatus",
    {
      headers: {
        Authorization: "Bearer YOUR_ACCESS_TOKEN",
      },
    }
  )
  .then((response) => {
    console.log("Response:", response.data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

#### Responses

| Code | Description |
| ---- | ----------- |
| 200  | OK          |

##### Example Response

```json
{
  "status": "success",
  "payment_status": "completed",
  "amount": 100.0
}
```

#### Notes

- Replace `{clientId}` and `{collectionRequestId}` with actual UUID values.
- Ensure proper authorization with an access token in the headers.
- Responses may include additional fields depending on the payment status.
