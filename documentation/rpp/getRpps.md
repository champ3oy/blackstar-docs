# Get Recurring Payment Plan Details

## Overview

The `Get Recurring Payment Plan Details` endpoint retrieves the details of an existing recurring payment plan by its ID. This endpoint requires three mandatory path parameters: `clientId`, `portfolioId`, and `id`. It returns comprehensive information about the recurring payment plan, including its allocations, frequency, status, and other metadata.

---

## Endpoint Details

### HTTP Method

**GET**

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

## Responses

### 200 OK

The request was successful, and the recurring payment plan details were retrieved.

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
  "planName": "Monthly Savings Plan",
  "frequency": "DAILY",
  "installmentAmount": 50,
  "startDate": "2025-03-25T12:15:26.816Z",
  "endDate": "2026-03-25T12:15:26.816Z",
  "status": "ACTIVE",
  "archived": false,
  "otpReferenceId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

#### Response Fields

| Field                    | Type    | Description                                                                                                                                                    |
| ------------------------ | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                     | string  | Unique identifier for the recurring payment plan.                                                                                                              |
| `customerMsisdn`         | string  | The mobile number of the customer associated with the plan.                                                                                                    |
| `securityAllocations`    | array   | List of security allocations for the plan.                                                                                                                     |
| - `securityUUID`         | string  | Unique identifier for the security.                                                                                                                            |
| - `allocationPercentage` | number  | Percentage of the allocation for the security.                                                                                                                 |
| - `securitySymbol`       | string  | Symbol or identifier for the security.                                                                                                                         |
| `planName`               | string  | Name of the recurring payment plan.                                                                                                                            |
| `frequency`              | string  | Frequency of the payments (e.g., DAILY, WEEKLY, MONTHLY, QUARTERLY).                                                                                           |
| `installmentAmount`      | number  | Amount of each installment.                                                                                                                                    |
| `startDate`              | string  | Start date of the recurring payment plan in ISO 8601 format.                                                                                                   |
| `endDate`                | string  | End date of the recurring payment plan in ISO 8601 format.                                                                                                     |
| `status`                 | string  | Current status of the plan (ACTIVE, PENDING_VERIFICATION_PREAPPROVAL_OTP, PENDING_VERIFICATION_OTP, INACTIVE, PENDING_VERIFICATION_PREAPPROVAL_USSD, EXPIRED). |
| `archived`               | boolean | Indicates whether the plan is archived.                                                                                                                        |
| `otpReferenceId`         | string  | Reference ID for OTP verification (if applicable).                                                                                                             |

---

### 404 Not Found

The recurring payment plan with the specified ID was not found.

#### Example Response Body

```json
{
  "message": "Recurring payment plan not found"
}
```

---

## Examples

### CURL Example

```bash
curl -X GET "https://api.example.com/api/rpp/client/{clientId}/portfolio/{portfolioId}/{id}" \
-H "Accept: */*"
```

#### Explanation:

- Replace `{clientId}`, `{portfolioId}`, and `{id}` with valid UUIDs.
- The `Accept` header is set to `*/*`.

---

### JavaScript (Axios) Example

```javascript
const axios = require("axios");

const clientId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual client UUID
const portfolioId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual portfolio UUID
const id = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual recurring payment plan UUID

axios
  .get(
    `https://api.example.com/api/rpp/client/${clientId}/portfolio/${portfolioId}/${id}`,
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

- Replace `clientId`, `portfolioId`, and `id` with valid UUIDs.
- The `Accept` header is set to `*/*`.

---

## Notes

1. Ensure that the `clientId`, `portfolioId`, and `id` are valid UUIDs.
2. The `frequency` field specifies how often the recurring payment occurs. Possible values include:
   - `DAILY`: Payments occur daily.
   - `WEEKLY`: Payments occur weekly.
   - `MONTHLY`: Payments occur monthly.
3. The `status` field indicates the current state of the recurring payment plan. Common values include:
   - `ACTIVE`: The plan is currently active.
   - `INACTIVE`: The plan is inactive.
4. If the `archived` field is `true`, the plan has been archived and is no longer in use.
5. The `otpReferenceId` can be used for further actions, such as OTP validation, if applicable.
