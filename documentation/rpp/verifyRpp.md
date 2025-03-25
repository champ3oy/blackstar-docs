# Verify Recurring Payment Plan

## Overview

The `Verify Recurring Payment Plan` endpoint triggers an OTP (One-Time Password) or USSD prompt to authenticate and verify a recurring payment plan based on its status. This endpoint requires three mandatory path parameters: `clientId`, `portfolioId`, and `rppId`. It is used to initiate verification for recurring payment plans with specific statuses:

- **PENDING_VERIFICATION_PREAPPROVAL_OTP**: An OTP will be sent from Hubtel.
- **PENDING_VERIFICATION_PREAPPROVAL_USSD**: A USSD prompt will be initiated from Hubtel.
- **PENDING_VERIFICATION_OTP**: If the preapproval is already approved, an OTP will be sent from our end.

Upon successful verification initiation, it confirms that the OTP or USSD prompt has been sent.

---

## Endpoint Details

### HTTP Method

**POST**

### URL

```
/api/rpp/client/{clientId}/portfolio/{portfolioId}/{rppId}/verify-rpp
```

---

## Parameters

| Name          | Description                 | Type   | Format | Required | Location |
| ------------- | --------------------------- | ------ | ------ | -------- | -------- |
| `clientId`    | Client UUID                 | string | $uuid  | Yes      | Path     |
| `portfolioId` | Portfolio UUID              | string | $uuid  | Yes      | Path     |
| `rppId`       | Recurring Payment Plan UUID | string | $uuid  | Yes      | Path     |

---

## Responses

### 200 OK

The request was successful, and the OTP or USSD prompt was sent.

#### Example Response Body

```json
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "customerMsisdn": "string",
  "securityAllocations": [
    {
      "securityUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "allocationPercentage": 100,
      "securitySymbol": "string"
    }
  ],
  "planName": "string",
  "frequency": "DAILY",
  "installmentAmount": 0,
  "startDate": "2025-03-25T12:26:33.481Z",
  "endDate": "2025-03-25T12:26:33.481Z",
  "status": "ACTIVE",
  "archived": true,
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
| `planName`               | string  | Name of the recurring payment plan.                                                                                                                          |
| `frequency`              | string  | Frequency of the payments (e.g., DAILY, WEEKLY, MONTHLY).                                                                                                    |
| `installmentAmount`      | number  | Amount of each installment.                                                                                                                                  |
| `startDate`              | string  | Start date of the recurring payment plan in ISO 8601 format.                                                                                                 |
| `endDate`                | string  | End date of the recurring payment plan in ISO 8601 format.                                                                                                   |
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
  "details": "The 'clientId' must be a valid UUID."
}
```

---

### 409 Conflict

The preapproval is already approved, and no further verification is required.

#### Example Response Body

```json
{
  "error": "Preapproval already approved",
  "details": "No further verification is required for this recurring payment plan."
}
```

---

## Examples

### CURL Example

```bash
curl -X POST "https://api.example.com/api/rpp/client/{clientId}/portfolio/{portfolioId}/{rppId}/verify-rpp" \
-H "Accept: */*"
```

#### Explanation:

- Replace `{clientId}`, `{portfolioId}`, and `{rppId}` with valid UUIDs.
- The `Accept` header is set to `*/*`.

---

### JavaScript (Axios) Example

```javascript
const axios = require("axios");

const clientId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual client UUID
const portfolioId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual portfolio UUID
const rppId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual recurring payment plan UUID

axios
  .post(
    `https://api.example.com/api/rpp/client/${clientId}/portfolio/${portfolioId}/${rppId}/verify-rpp`,
    null,
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

- Replace `clientId`, `portfolioId`, and `rppId` with valid UUIDs.
- The `Accept` header is set to `*/*`.

---

## Notes

1. Ensure that the `clientId`, `portfolioId`, and `rppId` are valid UUIDs.
2. The endpoint initiates verification based on the status of the recurring payment plan:
   - For `PENDING_VERIFICATION_PREAPPROVAL_OTP`, an OTP will be sent from Hubtel.
   - For `PENDING_VERIFICATION_PREAPPROVAL_USSD`, a USSD prompt will be initiated from Hubtel.
   - For `PENDING_VERIFICATION_OTP`, an OTP will be sent from our end if the preapproval is already approved.
3. If the verification fails, check the error message in the response for details on why the operation was unsuccessful.
