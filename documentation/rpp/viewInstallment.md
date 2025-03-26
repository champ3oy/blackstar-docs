# Get Recurring Payment Plan Passbook

## Overview

The `Get Recurring Payment Plan Passbook` endpoint retrieves the passbook entries for a specific recurring payment plan. The passbook includes transaction details based on the statuses provided in the request body. This endpoint requires three mandatory path parameters: `clientId`, `portfolioId`, and `rppId`.

---

## Endpoint Details

### HTTP Method

**POST**

### URL

```
/api/rpp/client/{clientId}/portfolio/{portfolioId}/{rppId}/passbook
```

---

## Parameters

| Name          | Description                 | Type   | Format | Required | Location |
| ------------- | --------------------------- | ------ | ------ | -------- | -------- |
| `clientId`    | Client UUID                 | string | $uuid  | Yes      | Path     |
| `portfolioId` | Portfolio UUID              | string | $uuid  | Yes      | Path     |
| `rppId`       | Recurring Payment Plan UUID | string | $uuid  | Yes      | Path     |

---

## Request Body

The request body must be in `application/json` format and includes the following field:

| Field      | Type  | Description                                      |
| ---------- | ----- | ------------------------------------------------ |
| `statuses` | array | List of statuses to filter the passbook entries. |

#### Example Request Body

```json
{
  "statuses": ["PENDING"]
}
```

---

## Responses

### 200 OK

The request was successful, and the passbook entries were retrieved.

#### Example Response Body

```json
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "entries": [
    {
      "transactionId": "txn12345",
      "status": "PENDING",
      "amount": 100.0,
      "date": "25-03-2025T12:30:00Z"
    }
  ]
}
```

#### Response Fields

| Field             | Type   | Description                                                                                                               |
| ----------------- | ------ | ------------------------------------------------------------------------------------------------------------------------- |
| `id`              | string | Unique identifier for the recurring payment plan.                                                                         |
| `entries`         | array  | List of passbook entries.                                                                                                 |
| - `transactionId` | string | Unique identifier for the transaction.                                                                                    |
| - `status`        | string | Status of the transaction (e.g., PENDING, COMPLETED, FAILED,PROCESSING, PENDING_PAYMENT_CONFIRMATION, PAYMENT_CONFIRMED). |
| - `amount`        | number | Amount of the transaction.                                                                                                |
| - `date`          | string | Date and time of the transaction in ISO 8601 format.                                                                      |

---

### 400 Bad Request

The request contains invalid input data.

#### Example Response Body

```json
{
  "error": "Invalid input data",
  "details": "The 'statuses' field must be a non-empty array."
}
```

---

## Examples

### CURL Example

```bash
curl -X POST "https://api.example.com/api/rpp/client/{clientId}/portfolio/{portfolioId}/{rppId}/passbook" \
-H "Content-Type: application/json" \
-H "Accept: */*" \
-d '{
  "statuses": ["PENDING"]
}'
```

#### Explanation:

- Replace `{clientId}`, `{portfolioId}`, and `{rppId}` with valid UUIDs.
- The `Content-Type` header is set to `application/json`.
- The `-d` flag specifies the JSON payload containing the statuses to filter the passbook entries.

---

### JavaScript (Axios) Example

```javascript
const axios = require("axios");

const clientId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual client UUID
const portfolioId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual portfolio UUID
const rppId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual recurring payment plan UUID

const requestData = {
  statuses: ["PENDING"],
};

axios
  .post(
    `https://api.example.com/api/rpp/client/${clientId}/portfolio/${portfolioId}/${rppId}/passbook`,
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

- Replace `clientId`, `portfolioId`, and `rppId` with valid UUIDs.
- The `requestData` object contains the JSON payload for the request body.
- The `Content-Type` and `Accept` headers are set appropriately.

---

## Notes

1. Ensure that the `clientId`, `portfolioId`, and `rppId` are valid UUIDs.
2. The `statuses` field in the request body should be a non-empty array of valid transaction statuses.
3. If the request fails, check the error message in the response for details on why the operation was unsuccessful.
