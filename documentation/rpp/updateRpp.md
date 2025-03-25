# Update Recurring Payment Plan

## Overview

The `Update Recurring Payment Plan` endpoint allows you to modify an existing recurring payment plan by its ID. This endpoint requires three mandatory path parameters: `clientId`, `portfolioId`, and `id`. It also accepts a JSON request body containing the fields to be updated. Upon successful update, it returns the updated details of the recurring payment plan.

---

## Endpoint Details

### HTTP Method

**PUT**

### URL

```
/api/rpp/client/{clientId}/portfolio/{portfolioId}/{id}
```

---

## Parameters

| Name          | Description                 | Type   | Format | Required | Location |
| ------------- | --------------------------- | ------ | ------ | -------- | -------- |
| `clientId`    | Client UUID                 | string | $uuid  | Yes      | Path     |
| `portfolioId` | Portfolio UUID              | string | $uuid  | Yes      | Path     |
| `id`          | Recurring Payment Plan UUID | string | $uuid  | Yes      | Path     |

---

## Request Body

The request body must be in `application/json` format and can include the following fields:

| Field               | Type   | Description                                                            |
| ------------------- | ------ | ---------------------------------------------------------------------- |
| `planName`          | string | The updated name of the recurring payment plan.                        |
| `installmentAmount` | number | The updated amount of each installment.                                |
| `endDate`           | string | The updated end date of the recurring payment plan in ISO 8601 format. |

#### Example Request Body

```json
{
  "planName": "Updated Monthly Savings Plan",
  "installmentAmount": 75.5,
  "endDate": "2026-03-25T12:18:19.292Z"
}
```

---

## Responses

### 200 OK

The request was successful, and the recurring payment plan was updated.

#### Example Response Body

```json
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "customerMsisdn": "233123456789",
  "securityAllocations": [
    {
      "securityUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "allocationPercentage": 100,
      "securitySymbol": "SEC123"
    }
  ],
  "planName": "Updated Monthly Savings Plan",
  "frequency": "DAILY",
  "installmentAmount": 75.5,
  "startDate": "2025-03-25T12:18:19.293Z",
  "endDate": "2026-03-25T12:18:19.293Z",
  "status": "ACTIVE",
  "archived": false,
  "otpReferenceId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

#### Response Fields

| Field                    | Type    | Description                                                                                                                                                  |
| ------------------------ | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `id`                     | string  | Unique identifier for the recurring payment plan.                                                                                                            |
| `customerMsisdn`         | string  | The mobile number of the customer associated with the plan.                                                                                                  |
| `securityAllocations`    | array   | List of security allocations for the plan.                                                                                                                   |
| - `securityUUID`         | string  | Unique identifier for the security.                                                                                                                          |
| - `allocationPercentage` | number  | Percentage of the allocation for the security.                                                                                                               |
| - `securitySymbol`       | string  | Symbol or identifier for the security.                                                                                                                       |
| `planName`               | string  | Updated name of the recurring payment plan.                                                                                                                  |
| `frequency`              | string  | Frequency of the payments (e.g., DAILY, WEEKLY, MONTHLY).                                                                                                    |
| `installmentAmount`      | number  | Updated amount of each installment.                                                                                                                          |
| `startDate`              | string  | Start date of the recurring payment plan in ISO 8601 format.                                                                                                 |
| `endDate`                | string  | Updated end date of the recurring payment plan in ISO 8601 format.                                                                                           |
| `status`                 | string  | Current status of the plan ACTIVE, PENDING_VERIFICATION_PREAPPROVAL_OTP, PENDING_VERIFICATION_OTP, INACTIVE, PENDING_VERIFICATION_PREAPPROVAL_USSD, EXPIRED. |
| `archived`               | boolean | Indicates whether the plan is archived.                                                                                                                      |
| `otpReferenceId`         | string  | Reference ID for OTP verification (if applicable).                                                                                                           |

---

### 400 Bad Request

The request contains invalid input data.

#### Example Response Body

```json
{
  "error": "Invalid input data",
  "details": "The 'installmentAmount' must be greater than zero."
}
```

---

### 404 Not Found

The recurring payment plan with the specified ID was not found.

#### Example Response Body

```json
{
  "error": "Recurring payment plan not found",
  "details": "No recurring payment plan exists with the provided ID."
}
```

---

## Examples

### CURL Example

```bash
curl -X PUT "https://api.example.com/api/rpp/client/{clientId}/portfolio/{portfolioId}/{id}" \
-H "Content-Type: application/json" \
-H "Accept: */*" \
-d '{
  "planName": "Updated Monthly Savings Plan",
  "installmentAmount": 75.5,
  "endDate": "2026-03-25T12:18:19.292Z"
}'
```

#### Explanation:

- Replace `{clientId}`, `{portfolioId}`, and `{id}` with valid UUIDs.
- The `Content-Type` header is set to `application/json`.
- The `-d` flag specifies the JSON request body containing the fields to be updated.

---

### JavaScript (Axios) Example

```javascript
const axios = require("axios");

const clientId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual client UUID
const portfolioId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual portfolio UUID
const id = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual recurring payment plan UUID

const requestData = {
  planName: "Updated Monthly Savings Plan",
  installmentAmount: 75.5,
  endDate: "2026-03-25T12:18:19.292Z",
};

axios
  .put(
    `https://api.example.com/api/rpp/client/${clientId}/portfolio/${portfolioId}/${id}`,
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

- Replace `clientId`, `portfolioId`, and `id` with valid UUIDs.
- The `requestData` object contains the JSON payload for the request body.
- The `Content-Type` and `Accept` headers are set appropriately.

---

## Notes

1. Ensure that the `clientId`, `portfolioId`, and `id` are valid UUIDs.
2. Only the fields included in the request body will be updated. Fields not included in the request body will remain unchanged.
3. The `installmentAmount` must be greater than zero.
4. The `endDate` must be a valid ISO 8601 date and should not be earlier than the `startDate`.
5. If the update fails, check the error message in the response for details on why the operation was unsuccessful.
