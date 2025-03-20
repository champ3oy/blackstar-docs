# Direct Receive Money

## Overview

The `Direct Receive Money` endpoint is used to initiate a mobile money collection request for a specific client and portfolio. This endpoint requires two mandatory path parameters (`clientId` and `portfolioId`) and a JSON request body containing details such as the amount, success/fail URLs, and security allocations.

---

## Endpoint Details

### HTTP Method

**POST**

### URL

```
/api/client/{clientId}/portfolio/{portfolioId}/mobile-money/collectionRequest
```

---

## Parameters

| Name          | Description    | Type   | Format | Required | Location |
| ------------- | -------------- | ------ | ------ | -------- | -------- |
| `clientId`    | Client UUID    | string | $uuid  | Yes      | Path     |
| `portfolioId` | Portfolio UUID | string | $uuid  | Yes      | Path     |

---

## Request Body

The request body must be in `application/json` format and include the following fields:

| Field                    | Type           | Description                                                |
| ------------------------ | -------------- | ---------------------------------------------------------- |
| `amount`                 | number         | The amount to be collected.                                |
| `successUrl`             | string         | URL to redirect to upon successful transaction completion. |
| `failUrl`                | string         | URL to redirect to if the transaction fails.               |
| `securityId`             | string ($uuid) | Security identifier associated with the transaction.       |
| `mobileMoneyId`          | string ($uuid) | Mobile money account identifier.                           |
| `clientReference`        | string         | Reference ID provided by the client for tracking purposes. |
| `webhookURL`             | string         | URL to which transaction status updates will be sent.      |
| `securityAllocations`    | array          | List of security allocations, each containing:             |
| - `securityUUID`         | string ($uuid) | Unique identifier for the security.                        |
| - `allocationPercentage` | number         | Percentage of the amount allocated to the security.        |

#### Example Request Body

```json
{
  "amount": 100,
  "successUrl": "https://example.com/success",
  "failUrl": "https://example.com/failure",
  "securityId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "mobileMoneyId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "clientReference": "ref12345",
  "webhookURL": "https://example.com/webhook",
  "securityAllocations": [
    {
      "securityUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "allocationPercentage": 100
    }
  ]
}
```

#### Webhook Data

Payment event

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

Order event

```json
{
  "eventType": "ORDER_STATUS",
  "timeStamp": "13-03-2025 05:47",
  "clientOrderId": "04ef5a6b-2dc4-4e6d-bc04-df3134099f1e",
  "orderSide": "SELL",
  "clientOrderStatus": "EXECUTED",
  "executedQuantity": 0.0648305,
  "executedConsiderationWithCurrency": 10.0,
  "executedAvgPrice": 154.2483,
  "orderDate": "24-02-2025",
  "clientReference": null
}
```

---

## Responses

### 200 OK

The request was successful, and the collection request was initiated.

#### Example Response Body

```json
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "portfolioId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "portfolioName": "Sample Portfolio",
  "hubtleConfigId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "amount": 100,
  "charges": 5,
  "transactionId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "requestType": "ONLINE_CHECKOUT_COLLECTION",
  "status": "SUBMITTED",
  "executionErrorMessage": "",
  "description": "Collection request submitted successfully",
  "valueDate": "2025-03-20T11:56:50.642Z",
  "custodianId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

#### Response Fields

| Field                   | Type   | Description                                          |
| ----------------------- | ------ | ---------------------------------------------------- |
| `id`                    | string | Unique identifier for the transaction.               |
| `portfolioId`           | string | Identifier for the portfolio.                        |
| `portfolioName`         | string | Name of the portfolio.                               |
| `hubtleConfigId`        | string | Configuration ID for the hubtle service.             |
| `amount`                | number | Amount requested for collection.                     |
| `charges`               | number | Transaction charges applied.                         |
| `transactionId`         | string | Unique identifier for the transaction.               |
| `requestType`           | string | Type of request (e.g., ONLINE_CHECKOUT_COLLECTION).  |
| `status`                | string | Current status of the transaction (e.g., SUBMITTED). |
| `executionErrorMessage` | string | Error message if execution fails.                    |
| `description`           | string | Description of the transaction.                      |
| `valueDate`             | string | Date and time of the transaction.                    |
| `custodianId`           | string | Identifier for the custodian.                        |

---

## Examples

### CURL Example

```bash
curl -X POST "https://api.example.com/api/client/{clientId}/portfolio/{portfolioId}/mobile-money/collectionRequest" \
-H "Content-Type: application/json" \
-H "Accept: */*" \
-d '{
  "amount": 100,
  "successUrl": "https://example.com/success",
  "failUrl": "https://example.com/failure",
  "securityId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "mobileMoneyId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "clientReference": "ref12345",
  "webhookURL": "https://example.com/webhook",
  "securityAllocations": [
    {
      "securityUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "allocationPercentage": 100
    }
  ]
}'
```

#### Explanation:

- Replace `{clientId}` and `{portfolioId}` with valid UUIDs.
- The `Content-Type` header is set to `application/json`.
- The `-d` flag specifies the JSON request body.

---

### JavaScript (Axios) Example

```javascript
const axios = require("axios");

const clientId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual client UUID
const portfolioId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual portfolio UUID

const requestData = {
  amount: 100,
  successUrl: "https://example.com/success",
  failUrl: "https://example.com/failure",
  securityId: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  mobileMoneyId: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  clientReference: "ref12345",
  webhookURL: "https://example.com/webhook",
  securityAllocations: [
    {
      securityUUID: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      allocationPercentage: 100,
    },
  ],
};

axios
  .post(
    `https://api.example.com/api/client/${clientId}/portfolio/${portfolioId}/mobile-money/collectionRequest`,
    requestData,
    {
      headers: {
        "Content-Type": "application/json",
        Accept: "*/*",
      },
    }
  )
  .then((response) => {
    console.log("Response:", response.data);
  })
  .catch((error) => {
    console.error(
      "Error:",
      error.response ? error.response.data : error.message
    );
  });
```

#### Explanation:

- Replace `clientId` and `portfolioId` with valid UUIDs.
- The `requestData` object contains the JSON payload for the request body.
- The `Content-Type` and `Accept` headers are set appropriately.

---

## Notes

1. Ensure that the `clientId` and `portfolioId` are valid UUIDs.
2. The `successUrl` and `failUrl` should be valid URLs where users will be redirected based on the transaction outcome.
3. The `securityAllocations` array must contain at least one valid allocation with a `securityUUID` and `allocationPercentage`.
