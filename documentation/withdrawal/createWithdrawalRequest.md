# Create Withdrawal Request

## Overview

Creates a withdrawal request for a specified client and portfolio.

### Endpoint

- **METHOD**: `POST`
- **PATH**: `/api/client/{clientId}/portfolio/{portfolioId}/withdrawalRequest/create`

#### Parameters

| Name        | Type   | Description                     |
| ----------- | ------ | ------------------------------- |
| clientId    | string | Client UUID (path parameter)    |
| portfolioId | string | Portfolio UUID (path parameter) |

#### Request Body

- **Content Type**: application/json

```json
{
  "amount": 0,
  "accountId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "description": "string",
  "lastDigitsOfAccount": "string"
}
```

#### Responses

| Code | Description | Example Response Body |
| ---- | ----------- | --------------------- |
| 200  | OK          | See example below     |

##### Example Response Body (200 OK)

```json
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "portfolioId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "portfolioName": "string",
  "hubtleConfigId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "amount": 0,
  "transactionId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "requestType": "COLLECTION",
  "status": "SUBMITTED",
  "executionErrorMessage": "string",
  "description": "string",
  "valueDate": "2024-07-02T10:48:35.678Z",
  "custodianId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

#### Example Requests

##### CURL

```bash
curl -X POST "https://api.uatdev.blackstargroup.ai/api/client/{clientId}/portfolio/{portfolioId}/withdrawalRequest/create" \
-H "Content-Type: application/json" \
-d '{
  "amount": 0,
  "accountId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "description": "string",
  "lastDigitsOfAccount": "string"
}'
```

##### JavaScript (Axios)

```javascript
const axios = require("axios");

axios
  .post(
    "https://api.uatdev.blackstargroup.ai/api/client/{clientId}/portfolio/{portfolioId}/withdrawalRequest/create",
    {
      amount: 0,
      accountId: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      description: "string",
      lastDigitsOfAccount: "string",
    }
  )
  .then((response) => {
    console.log("Response:", response.data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

#### Notes

- Ensure `clientId` and `portfolioId` are valid UUIDs.
- The request body requires `amount`, `accountId`, `description`, and `lastDigitsOfAccount` fields.
- The response includes various details of the created withdrawal request, including status and identifiers.
