## Create Collection Request

### Overview

This API endpoint allows the creation of a collection request for a specified client and portfolio. It returns a payment link which you show to the client to complete payment.

### Endpoint

`POST /api/client/{clientId}/portfolio/{portfolioId}/collectionRequest/create`

### Parameters

| Name        | Type   | Location | Description    |
| ----------- | ------ | -------- | -------------- |
| clientId    | string | path     | Client UUID    |
| portfolioId | string | path     | Portfolio UUID |

### Request Body

| Name         | Type   | Description                   |
| ------------ | ------ | ----------------------------- |
| amount       | number | The amount to be collected.   |
| successUrl   | string | URL to redirect upon success. |
| failUrl      | string | URL to redirect upon failure. |
| securityId   | string | UUID of the security.         |
| orderOfferId | string | UUID of the order offer.      |

### Example Request Body

```json
{
  "amount": 0,
  "successUrl": "string",
  "failUrl": "string",
  "securityId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "orderOfferId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

### Response Body

| Name        | Type   | Description               |
| ----------- | ------ | ------------------------- |
| redirectUrl | string | URL to redirect the user. |

### Example Response Body

```json
{
  "redirectUrl": "string"
}
```

### CURL Example

```sh
curl -X POST "https://api.uatdev.blackstargroup.ai/api/client/{clientId}/portfolio/{portfolioId}/collectionRequest/create" \
-H "Content-Type: application/json" \
-d '{
  "amount": 0,
  "successUrl": "https://example.com/success",
  "failUrl": "https://example.com/fail",
  "securityId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "orderOfferId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}'
```

### JavaScript Axios Example

```javascript
const axios = require("axios");

const clientId = "your-client-id";
const portfolioId = "your-portfolio-id";
const data = {
  amount: 0,
  successUrl: "https://example.com/success",
  failUrl: "https://example.com/fail",
  securityId: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  orderOfferId: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
};

axios
  .post(
    `https://api.uatdev.blackstargroup.ai/api/client/${clientId}/portfolio/${portfolioId}/collectionRequest/create`,
    data,
    {
      headers: {
        "Content-Type": "application/json",
      },
    }
  )
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

### Notes

- Ensure that the `clientId` and `portfolioId` are valid UUIDs.
- The `amount` should be a non-negative number.
- The `successUrl` and `failUrl` should be valid URLs.
- The `securityId` and `orderOfferId` should be valid UUIDs.

### Details

The `successUrl` and `failUrl` are used to redirect the user based on the payment status. The `securityId` and `orderOfferId` are necessary to identify the specific security and order offer related to the collection request.
