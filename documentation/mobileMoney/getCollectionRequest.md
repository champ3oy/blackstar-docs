# Get Collection Request

## Overview

The `Get Collection Request` endpoint retrieves details of a specific collection request associated with a client. This endpoint requires two mandatory path parameters: `clientId` and `collectionRequestId`. It returns detailed information about the collection request, including its status, transaction ID, and other metadata.

---

## Endpoint Details

### HTTP Method

**GET**

### URL

```
/api/client/{clientId}/collectionRequest/{collectionRequestId}
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

The request was successful, and the collection request details were retrieved.

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
  "valueDate": "2025-03-20T12:07:38.450Z",
  "custodianId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

#### Response Fields

| Field                   | Type   | Description                                                 |
| ----------------------- | ------ | ----------------------------------------------------------- |
| `id`                    | string | Unique identifier for the collection request.               |
| `portfolioId`           | string | Identifier for the portfolio associated with the request.   |
| `portfolioName`         | string | Name of the portfolio.                                      |
| `hubtleConfigId`        | string | Configuration ID for the hubtle service.                    |
| `amount`                | number | Amount requested for collection.                            |
| `charges`               | number | Transaction charges applied.                                |
| `transactionId`         | string | Unique identifier for the transaction.                      |
| `requestType`           | string | Type of request (e.g., ONLINE_CHECKOUT_COLLECTION).         |
| `status`                | string | Current status of the collection request (e.g., SUBMITTED). |
| `executionErrorMessage` | string | Error message if execution fails.                           |
| `description`           | string | Description of the collection request.                      |
| `valueDate`             | string | Date and time of the transaction in ISO 8601 format.        |
| `custodianId`           | string | Identifier for the custodian.                               |

---

## Examples

### CURL Example

```bash
curl -X GET "https://api.example.com/api/client/{clientId}/collectionRequest/{collectionRequestId}" \
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
    `https://api.example.com/api/client/${clientId}/collectionRequest/${collectionRequestId}`,
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
2. The `status` field indicates the current state of the collection request (e.g., `SUBMITTED`, `COMPLETED`, `FAILED`).
3. If the `executionErrorMessage` field is not empty, it provides details about any errors that occurred during the execution of the collection request.
4. The `valueDate` field represents the timestamp of the transaction in UTC.
