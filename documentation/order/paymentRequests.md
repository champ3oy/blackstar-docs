# Check Payment Status

## Overview

This API endpoint allows you to check the status of payment requests by providing the necessary identifiers (`clientId` and `portfolioId`) along with additional query parameters and a request body.

### HTTP Method

**POST**

### Endpoint URL

```
/api/client/{clientId}/portfolio/{portfolioId}/paymentRequest/search
```

### Parameters

| Name        | Type    | Format | Required | Description                |
| ----------- | ------- | ------ | -------- | -------------------------- |
| clientId    | string  | $uuid  | Yes      | Client UUID                |
| portfolioId | string  | $uuid  | Yes      | Portfolio UUID             |
| page        | integer | $int32 | Yes      | Page number for pagination |
| size        | integer | $int32 | Yes      | Number of items per page   |

### Request Body Parameters

| Field Name             | Type             | Format/Example                           | Required | Description                                                                                                                                                                                                             |
| ---------------------- | ---------------- | ---------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `assetClassList`       | Array of strings | `["BILL"]`                               | No       | List of asset classes to filter payment requests. e.g (BILL, BOND, CASH, FX, INDEX, BENCHMARK, CIS, VENTURE_CAPITAL, EQUITY, ETF, FD, REPO, STRUCTURED_TRADE, SWITCH, RECEIVABLE_LOAN, PAYABLE_LOAN, CRYPTO, COMMODITY) |
| `searchQuery`          | String           | `"string"`                               | No       | A search query string to filter results (e.g., by order ID or reference).                                                                                                                                               |
| `startDate`            | String           | `"2025-03-26T13:33:08.565Z"`             | No       | Start date for filtering payment requests (ISO 8601 format).                                                                                                                                                            |
| `endDate`              | String           | `"2025-03-26T13:33:08.565Z"`             | No       | End date for filtering payment requests (ISO 8601 format).                                                                                                                                                              |
| `settlementStatus`     | String           | `"NOT_INITIATED"`                        | No       | Settlement status of the payment request (e.g., NOT_INITIATED, INITIATED, SENT, SETTLED, FAILED, ERROR).                                                                                                                |
| `paymentType`          | String           | `"RTGS"`                                 | No       | Type of payment (e.g., RTGS, ACH, BT).                                                                                                                                                                                  |
| `authStatuses`         | Array of strings | `["APPROVED"]`                           | No       | List of authorization statuses to filter payment requests (e.g: APPROVED, PENDING_APPROVAL, REJECTED).                                                                                                                  |
| `portfolioId`          | String           | `"3fa85f64-5717-4562-b3fc-2c963f66afa6"` | No       | Portfolio UUID to filter payment requests.                                                                                                                                                                              |
| `clientId`             | String           | `"3fa85f64-5717-4562-b3fc-2c963f66afa6"` | No       | Client UUID to filter payment requests.                                                                                                                                                                                 |
| `clientOrderId`        | String           | `"3fa85f64-5717-4562-b3fc-2c963f66afa6"` | No       | Client order ID to filter payment requests.                                                                                                                                                                             |
| `clientOrderReference` | String           | `"string"`                               | No       | Client order reference to filter payment requests.                                                                                                                                                                      |
| `clientSubTypeId`      | String           | `"3fa85f64-5717-4562-b3fc-2c963f66afa6"` | No       | Client sub-type ID to filter payment requests.                                                                                                                                                                          |
| `showArchived`         | Boolean          | `true`                                   | No       | Whether to include archived payment requests in the results.                                                                                                                                                            |

### Request Body

The request body should be in JSON format with the following structure:

```json
{
  "assetClassList": ["BILL"],
  "searchQuery": "string",
  "startDate": "26-03-2025",
  "endDate": "26-03-2025",
  "settlementStatus": "NOT_INITIATED",
  "paymentType": "RTGS",
  "authStatuses": ["APPROVED"],
  "portfolioId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "clientId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "clientOrderId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "clientOrderReference": "string",
  "clientSubTypeId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "showArchived": true
}
```

### Responses

#### 200 OK

The payment status was successfully retrieved.

**Example Response:**

```json
{
  "totalElements": 0,
  "totalPages": 0,
  "size": 0,
  "content": [
    {
      "paymentRequestId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "clientOrderId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "clientReference": "string",
      "transactionId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "quantity": 0,
      "valueDate": "2025-03-26T13:33:08.566Z",
      "portfolioId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "status": "PENDING"
    }
  ],
  "number": 0,
  "sort": {
    "empty": true,
    "sorted": true,
    "unsorted": true
  },
  "numberOfElements": 0,
  "pageable": {
    "offset": 0,
    "sort": {
      "empty": true,
      "sorted": true,
      "unsorted": true
    },
    "pageSize": 0,
    "pageNumber": 0,
    "paged": true,
    "unpaged": true
  },
  "first": true,
  "last": true,
  "empty": true
}
```

### Notes

- Ensure that all required parameters are provided in the correct format.
- The `clientId` and `portfolioId` must be valid UUIDs.
- The `page` and `size` parameters are required for pagination.
- A successful response will return a `200 OK` with details of the payment requests.
