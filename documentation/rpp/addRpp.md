# Create Recurring Payment Plan

## Overview

The `Create Recurring Payment Plan` endpoint allows you to create a new recurring payment plan for a selected portfolio and securities. This endpoint requires two mandatory path parameters: `clientId` and `portfolioId`. It also accepts a JSON request body containing the details of the recurring payment plan. Upon successful creation, it returns the details of the newly created plan.

---

## Endpoint Details

### HTTP Method

**POST**

### URL

```
/api/rpp/client/{clientId}/portfolio/{portfolioId}
```

---

## Parameters

| Name          | Description    | Type   | Format | Required | Location |
| ------------- | -------------- | ------ | ------ | -------- | -------- |
| `clientId`    | Client UUID    | string | $uuid  | Yes      | Path     |
| `portfolioId` | Portfolio UUID | string | $uuid  | Yes      | Path     |

---

## Request Body

The request body must be in `application/json` format and includes the following fields:

| Field                    | Type   | Description                                                             |
| ------------------------ | ------ | ----------------------------------------------------------------------- |
| `customerMsisdn`         | string | The mobile number of the customer associated with the plan.             |
| `securityAllocations`    | array  | List of security allocations for the plan.                              |
| - `securityUUID`         | string | Unique identifier for the security.                                     |
| - `allocationPercentage` | number | Percentage of the allocation for the security(must add up to 100%).     |
| `planName`               | string | Name of the recurring payment plan.                                     |
| `frequency`              | string | Frequency of the payments (e.g., DAILY, WEEKLY, MONTHLY, QUARTERLY ).   |
| `installmentAmount`      | number | Amount of each installment.                                             |
| `endDate`                | string | End date of the recurring payment plan in ISO 8601 format(DD-MM-YYY).   |
| `channel`                | string | Payment channel (`MTN_GH_DIRECT_DEBIT` or `VODAFONE_GH_DIRECT_DEBIT `). |
| `startDate`              | string | Start date of the recurring payment plan in ISO 8601 format(DD-MM-YYY). |
| `mobileMoneyDetailId`    | string | Unique identifier for the mobile money detail of the user.              |

`Note:` `TIGO_GH`(AirtelTigo) is not supported for creating recurring payment plans

#### Example Request Body

```json
{
  "customerMsisdn": "0550000000",
  "securityAllocations": [
    {
      "securityUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "allocationPercentage": 100,
      "securitySymbol": "string",
      "logoPath": "string",
      "companyNameOrIssuer": "string"
    }
  ],
  "planName": "Monthly Savings Plan",
  "frequency": "DAILY",
  "installmentAmount": 50,
  "endDate": "2026-03-25",
  "channel": "MTN_GH_DIRECT_DEBIT",
  "startDate": "25-03-2025",
  "mobileMoneyDetailId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

---

## Responses

### 201 Created

The request was successful, and the recurring payment plan was created.

#### Example Response Body

```json
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "customerMsisdn": "0550000000",
  "securityAllocations": [
    {
      "securityUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "allocationPercentage": 100,
      "securitySymbol": "SEC123",
      "logoPath": "string",
      "companyNameOrIssuer": "string"
    }
  ],
  "planName": "Monthly Savings Plan",
  "frequency": "DAILY",
  "installmentAmount": 50,
  "startDate": "25-03-2025",
  "endDate": "2026-03-25",
  "status": "ACTIVE",
  "archived": false,
  "otpReferenceId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

#### Response Fields

| Field                   | Type    | Description                                                                                                                                                  |
| ----------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `id`                    | string  | Unique identifier for the recurring payment plan.                                                                                                            |
| `customerMsisdn`        | string  | The mobile number of the customer associated with the plan.                                                                                                  |
| `securityAllocations`   | array   | List of security allocations for the plan.                                                                                                                   |
| -`securityUUID`         | string  | Unique identifier for the security.                                                                                                                          |
| -`allocationPercentage` | number  | Percentage of the allocation for the security.                                                                                                               |
| -`securitySymbol`       | string  | Symbol or identifier for the security.                                                                                                                       |
| -`logoPath`             | string  | Logo for the security.                                                                                                                                       |
| -`companyNameOrIssuer`  | string  | Company name or Issuer for the security.                                                                                                                     |
| `planName`              | string  | Name of the recurring payment plan.                                                                                                                          |
| `frequency`             | string  | Frequency of the payments (e.g., DAILY, WEEKLY, MONTHLY, QUARTERLY).                                                                                         |
| `installmentAmount`     | number  | Amount of each installment.                                                                                                                                  |
| `startDate`             | string  | Start date of the recurring payment plan in ISO 8601 format(DD-MM-YYY).                                                                                      |
| `endDate`               | string  | End date of the recurring payment plan in ISO 8601 format(DD-MM-YYY).                                                                                        |
| `status`                | string  | Current status of the plan ACTIVE, PENDING_VERIFICATION_PREAPPROVAL_OTP, PENDING_VERIFICATION_OTP, INACTIVE, PENDING_VERIFICATION_PREAPPROVAL_USSD, EXPIRED. |
| `archived`              | boolean | Indicates whether the plan is archived.                                                                                                                      |
| `otpReferenceId`        | string  | Reference ID for OTP verification (if applicable).                                                                                                           |
| `installmentAmount`     | number  | Total completed installment amount                                                                                                                           |

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

## Examples

### CURL Example

```bash
curl -X POST "https://api.example.com/api/rpp/client/{clientId}/portfolio/{portfolioId}" \
-H "Content-Type: application/json" \
-H "Accept: */*" \
-d '{
  "customerMsisdn": "0550000000",
  "securityAllocations": [
    {
      "securityUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "allocationPercentage": 100,
    }
  ],
  "planName": "Monthly Savings Plan",
  "frequency": "DAILY",
  "installmentAmount": 50,
  "endDate": "2026-03-25",
  "channel": "MTN_GH_DIRECT_DEBIT",
  "startDate": "25-03-2025",
  "mobileMoneyDetailId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}'
```

#### Explanation:

- Replace `{clientId}` and `{portfolioId}` with valid UUIDs.
- The `Content-Type` header is set to `application/json`.
- The `-d` flag specifies the JSON request body containing the details of the recurring payment plan.

---

### JavaScript (Axios) Example

```javascript
const axios = require("axios");

const clientId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual client UUID
const portfolioId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual portfolio UUID

const requestData = {
  customerMsisdn: "0550000000",
  securityAllocations: [
    {
      securityUUID: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      allocationPercentage: 100,
    },
  ],
  planName: "Monthly Savings Plan",
  frequency: "DAILY",
  installmentAmount: 50,
  endDate: "2026-03-25",
  channel: "MTN_GH_DIRECT_DEBIT",
  startDate: "25-03-2025",
  mobileMoneyDetailId: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
};

axios
  .post(
    `https://api.example.com/api/rpp/client/${clientId}/portfolio/${portfolioId}`,
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
2. The `installmentAmount` must be greater than zero.
3. The `endDate` must be a valid ISO 8601 date and should not be earlier than the `startDate`.
4. The `channel` field specifies the payment method (e.g., `MTN_GH_DIRECT_DEBIT`).
5. If the creation fails, check the error message in the response for details on why the operation was unsuccessful.
6. Either mobileMoneyDetailId must be present OR both customerMsisdn and channel must be provided
7. StartDate mustbe the future date as first installment will be created on successful RPP verification
