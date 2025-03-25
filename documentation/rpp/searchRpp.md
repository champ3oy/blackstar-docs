# Search Recurring Payment Plans

## Overview

The `Search Recurring Payment Plans` endpoint allows you to retrieve recurring payment plans associated with a specific portfolio ID based on given search criteria. The search can be filtered by date ranges (`fromStartDate`, `toStartDate`, `fromEndDate`, `toEndDate`) and supports pagination.

---

## Endpoint Details

### HTTP Method

**POST**

### URL

```
/api/rpp/client/{clientId}/portfolio/{portfolioId}/search
```

---

## Parameters

| Name          | Description    | Type                                     | Format  | Required | Location |
| ------------- | -------------- | ---------------------------------------- | ------- | -------- | -------- |
| `clientId`    | Client UUID    | string                                   | $uuid   | Yes      | Path     |
| `portfolioId` | Portfolio UUID | string                                   | $uuid   | Yes      | Path     |
| `page`        | number         | Page number for pagination (default: 0). | integer | Yes      | Path     |
| `size`        | number         | Number of items per page (default: 10).  | integer | Yes      | Path     |

---

## Request Body

The request body must be in `application/json` format and includes the following fields:

| Field           | Type   | Description                                       |
| --------------- | ------ | ------------------------------------------------- |
| `fromStartDate` | string | Start date range for filtering (ISO 8601 format). |
| `toStartDate`   | string | End date range for filtering (ISO 8601 format).   |
| `fromEndDate`   | string | Start date range for filtering (ISO 8601 format). |
| `toEndDate`     | string | End date range for filtering (ISO 8601 format).   |
| `planName`      | string | Name of plan.                                     |
| `frequencyList` | array  | Array of frequencies. e.g.(["DAILY"]).            |
| `statusList`    | array  | Array of status. e.g.(["ACTIVE"]).                |
| `securityName`  | string | Name of security                                  |

#### Example Request Body

```json
{
  "fromStartDate": "2025-03-25T12:34:52.282Z",
  "toStartDate": "2025-03-25T12:34:52.282Z",
  "fromEndDate": "2025-03-25T12:34:52.282Z",
  "toEndDate": "2025-03-25T12:34:52.282Z",
  "page": 0,
  "size": 10
}
```

---

## Responses

### 200 OK

The request was successful, and the recurring payment plans were retrieved.

#### Example Response Body

```json
{
  "totalElements": 0,
  "content": [
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
      "startDate": "2025-03-25T12:34:52.284Z",
      "endDate": "2025-03-25T12:34:52.284Z",
      "status": "ACTIVE",
      "archived": true,
      "otpReferenceId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
    }
  ]
}
```

#### Response Fields

| Field                     | Type    | Description                                                                                                                                                  |
| ------------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `totalElements`           | number  | Total number of recurring payment plans matching the criteria.                                                                                               |
| `content`                 | array   | List of recurring payment plans.                                                                                                                             |
| - `id`                    | string  | Unique identifier for the recurring payment plan.                                                                                                            |
| - `customerMsisdn`        | string  | The mobile number of the customer associated with the plan.                                                                                                  |
| - `securityAllocations`   | array   | List of security allocations for the plan.                                                                                                                   |
| -- `securityUUID`         | string  | Unique identifier for the security.                                                                                                                          |
| -- `allocationPercentage` | number  | Percentage of the allocation for the security.                                                                                                               |
| -- `securitySymbol`       | string  | Symbol or identifier for the security.                                                                                                                       |
| - `planName`              | string  | Name of the recurring payment plan.                                                                                                                          |
| - `frequency`             | string  | Frequency of the payments (e.g., DAILY, WEEKLY, MONTHLY).                                                                                                    |
| - `installmentAmount`     | number  | Amount of each installment.                                                                                                                                  |
| - `startDate`             | string  | Start date of the recurring payment plan in ISO 8601 format.                                                                                                 |
| - `endDate`               | string  | End date of the recurring payment plan in ISO 8601 format.                                                                                                   |
| - `status`                | string  | Current status of the plan ACTIVE, PENDING_VERIFICATION_PREAPPROVAL_OTP, PENDING_VERIFICATION_OTP, INACTIVE, PENDING_VERIFICATION_PREAPPROVAL_USSD, EXPIRED. |
| - `archived`              | boolean | Indicates whether the plan is archived.                                                                                                                      |
| - `otpReferenceId`        | string  | Reference ID for OTP verification (if applicable).                                                                                                           |

---

### 400 Bad Request

The request contains invalid input data.

#### Example Response Body

```json
{
  "error": "Invalid input data",
  "details": "The 'fromStartDate' must be a valid ISO 8601 date."
}
```

---

## Examples

### CURL Example

```bash
curl -X POST "https://api.example.com/api/rpp/client/{clientId}/portfolio/{portfolioId}/search" \
-H "Content-Type: application/json" \
-H "Accept: */*" \
-d '{
  "fromStartDate": "2025-03-25T12:34:52.282Z",
  "toStartDate": "2025-03-25T12:34:52.282Z",
  "fromEndDate": "2025-03-25T12:34:52.282Z",
  "toEndDate": "2025-03-25T12:34:52.282Z",
  "page": 0,
  "size": 10
}'
```

#### Explanation:

- Replace `{clientId}` and `{portfolioId}` with valid UUIDs.
- The `Content-Type` header is set to `application/json`.
- The `-d` flag specifies the JSON payload containing the search criteria.

---

### JavaScript (Axios) Example

```javascript
const axios = require("axios");

const clientId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual client UUID
const portfolioId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual portfolio UUID

const requestData = {
  fromStartDate: "2025-03-25T12:34:52.282Z",
  toStartDate: "2025-03-25T12:34:52.282Z",
  fromEndDate: "2025-03-25T12:34:52.282Z",
  toEndDate: "2025-03-25T12:34:52.282Z",
  page: 0,
  size: 10,
};

axios
  .post(
    `https://api.example.com/api/rpp/client/${clientId}/portfolio/${portfolioId}/search`,
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
2. The date fields (`fromStartDate`, `toStartDate`, `fromEndDate`, `toEndDate`) must be in ISO 8601 format.
3. Pagination parameters (`page` and `size`) allow you to control the number of results returned.
4. If the request fails, check the error message in the response for details on why the operation was unsuccessful.
