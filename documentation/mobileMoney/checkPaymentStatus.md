# Check Payment Status

## Overview

The `Check Payment Status` endpoint is used to check the status of a specific payment associated with a collection request. This endpoint requires two mandatory path parameters: `clientId` and `collectionRequestId`. It returns the current status of the payment, allowing you to track whether the payment has been completed, failed, or is still pending.

---

## Endpoint Details

### HTTP Method

**GET**

### URL

```
/api/client/{clientId}/collectionRequest/{collectionRequestId}/checkStatus
```

---

## Parameters

| Name                  | Description             | Type   | Format | Required | Location |
| --------------------- | ----------------------- | ------ | ------ | -------- | -------- |
| `clientId`            | Client UUID             | string | $uuid  | Yes      | Path     |
| `collectionRequestId` | Collection Request UUID | string | $uuid  | Yes      | Path     |

---

## Responses

### 200 OK

The request was successful, and the payment status was retrieved.

#### Example Response Body

```json
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "status": "COMPLETED",
  "paymentDate": "2025-03-20T12:15:42.123Z",
  "amount": 100,
  "currency": "GHS",
  "transactionId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "errorMessage": "",
  "additionalDetails": {
    "providerReference": "REF12345",
    "paymentMethod": "MOBILE_MONEY"
  }
}
```

#### Response Fields

| Field               | Type   | Description                                                                      |
| ------------------- | ------ | -------------------------------------------------------------------------------- |
| `id`                | string | Unique identifier for the collection request.                                    |
| `status`            | string | Current status of the payment (e.g., COMPLETED, PENDING, FAILED).                |
| `paymentDate`       | string | Date and time of the payment in ISO 8601 format.                                 |
| `amount`            | number | Amount of the payment.                                                           |
| `currency`          | string | Currency of the payment (e.g., GHS, USD).                                        |
| `transactionId`     | string | Unique identifier for the transaction.                                           |
| `errorMessage`      | string | Error message if the payment fails.                                              |
| `additionalDetails` | object | Additional details about the payment (e.g., provider reference, payment method). |

---

## Examples

### CURL Example

```bash
curl -X GET "https://api.example.com/api/client/{clientId}/collectionRequest/{collectionRequestId}/checkStatus" \
-H "Accept: */*"
```

#### Explanation:

- Replace `{clientId}` and `{collectionRequestId}` with valid UUIDs.
- The `Accept` header is set to `*/*`.

---

### JavaScript (Axios) Example

```javascript
const axios = require("axios");

const clientId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual client UUID
const collectionRequestId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual collection request UUID

axios
  .get(
    `https://api.example.com/api/client/${clientId}/collectionRequest/${collectionRequestId}/checkStatus`,
    {
      headers: {
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

- Replace `clientId` and `collectionRequestId` with valid UUIDs.
- The `Accept` header is set to `*/*`.

---

## Notes

1. Ensure that the `clientId` and `collectionRequestId` are valid UUIDs.
2. The `status` field indicates the current state of the payment. Possible values include:
   - `PENDING`: Payment is still being processed.
   - `COMPLETED`: Payment has been successfully completed.
   - `FAILED`: Payment failed.
3. If the `errorMessage` field is not empty, it provides details about any issues encountered during the payment process.
4. The `additionalDetails` object may contain supplementary information, such as the provider's reference ID or the payment method used.
