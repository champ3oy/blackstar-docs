## Create Collection Request

### Overview

This API endpoint allows the creation of a collection request for a specified client and portfolio. It returns a payment link which you show to the client to complete payment.

> **New** 📢
> You can now add a webhook for payment collection status updates
> When an collection request is created, you can include a webhook URL in the request body

### Endpoint

`POST /api/client/{clientId}/portfolio/{portfolioId}/collectionRequest/create`

### Parameters

| Name        | Type   | Location | Description    |
| ----------- | ------ | -------- | -------------- |
| clientId    | string | path     | Client UUID    |
| portfolioId | string | path     | Portfolio UUID |

### Request Body

| Name                | Type   | Description                    |
| ------------------- | ------ | ------------------------------ |
| amount              | number | The amount to be collected.    |
| successUrl          | string | URL to redirect upon success.  |
| failUrl             | string | URL to redirect upon failure.  |
| securityId          | string | UUID of the security.          |
| mobileMoneyId       | string | ID for saved MoMo number.      |
| clientReference     | string | Clients reference.             |
| webhookURL          | string | Webhook URL for status update. |
| securityAllocations | string | Allocation for order.          |

### Example Request Body

```json
{
  "amount": 0,
  "successUrl": "string",
  "failUrl": "string",
  "securityId": "string",
  "mobileMoneyId": "string",
  "clientReference": "string",
  "webhookURL": "string",
  "securityAllocations": [
    {
      "securityUUID": "string",
      "allocationPercentage": 100
    }
  ]
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

### Webhook Data

```json
{
  "eventType": "DEPOSIT_STATUS",
  "timeStamp": "10-03-2025 12:42",
  "clientReference": "string1258",
  "transactionId": null,
  "amount": 0.1,
  "reasonForFailure": null,
  "status": "FAILED"
}
```

We will send an immediate webhook response. If the first attempt fails, we will retry after 5-10 minutes, followed by a second retry after another 5-10 minutes. In total, we will make up to three retry attempts.

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
  mobileMoneyId: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  webhookURL: "YOUR_WEBHOOK_URL",
  securityAllocations: [
    {
      securityUUID: "string",
      allocationPercentage: 100,
    },
  ],
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
