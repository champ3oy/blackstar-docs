## Cancel Recurring Payment Plan

### Overview

This API endpoint allows you to cancel an existing recurring payment plan by providing the necessary identifiers (`clientId`, `portfolioId`, and `id`).

### HTTP Method

**PATCH**

### Endpoint URL

```
/api/rpp/client/{clientId}/portfolio/{portfolioId}/{id}/cancel
```

### Parameters

| Name        | Type   | Format | Required | Description         |
| ----------- | ------ | ------ | -------- | ------------------- |
| clientId    | string | $uuid  | Yes      | Client UUID         |
| portfolioId | string | $uuid  | Yes      | Portfolio UUID      |
| id          | string | $uuid  | Yes      | Recurring plan UUID |

### Responses

#### 200 OK

The recurring payment plan was successfully canceled.

**Example Response:**

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
  "startDate": "2025-03-25T12:46:46.029Z",
  "endDate": "2025-03-25T12:46:46.029Z",
  "status": "ACTIVE",
  "archived": true,
  "otpReferenceId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

#### 404 Not Found

The specified recurring payment plan could not be found.

**Example Response:**

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
  "startDate": "2025-03-25T12:46:46.033Z",
  "endDate": "2025-03-25T12:46:46.033Z",
  "status": "ACTIVE",
  "archived": true,
  "otpReferenceId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

### Notes

- Ensure that all required parameters are provided in the correct format.
- The `clientId`, `portfolioId`, and `id` must be valid UUIDs.
- A successful cancellation will return a `200 OK` response with details of the canceled plan.
- If the recurring payment plan does not exist, a `404 Not Found` response will be returned.
