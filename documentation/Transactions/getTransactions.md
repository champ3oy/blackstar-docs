## Get Transactions

## Description

This API retrieves transactions for a specified client or portfolio.

## Endpoint

```
POST /api/client/{clientId}/transaction/search
```

## Parameters

| Name          | Type    | Description               | Required | Location |
| ------------- | ------- | ------------------------- | -------- | -------- |
| `clientId`    | string  | Client UUID               | Yes      | Path     |
| `portfolioId` | string  | Portfolio UUID            | No       | Query    |
| `page`        | integer | Current page              | Yes      | Query    |
| `size`        | integer | Maximum records per page  | Yes      | Query    |
| `sortBy`      | string  | Field to sort by          | No       | Query    |
| `sortDir`     | string  | Sort direction (ASC/DESC) | No       | Query    |

### Request Body

The request body should be a JSON object with the following fields:

| Name                             | Type    | Description                        | Required |
| -------------------------------- | ------- | ---------------------------------- | -------- |
| `assetClassList`                 | array   | List of asset classes              | No       |
| `searchQuery`                    | string  | Search query                       | No       |
| `startDate`                      | string  | Start date (ISO 8601 format)       | No       |
| `endDate`                        | string  | End date (ISO 8601 format)         | No       |
| `securityUUID`                   | string  | Security UUID                      | No       |
| `orderSide`                      | string  | Order side (e.g., BUY, SELL)       | No       |
| `corporateAction`                | string  | Corporate action type              | No       |
| `accountId`                      | string  | Account UUID                       | No       |
| `authStatuses`                   | array   | List of authorization statuses     | No       |
| `executionStatuses`              | array   | List of execution statuses         | No       |
| `showSystemGeneratedTransaction` | boolean | Show system-generated transactions | No       |
| `brokerTransactionsOnly`         | boolean | Show broker transactions only      | No       |
| `transactionTypeIds`             | array   | List of transaction type IDs       | No       |

### Example Request Body

```json
{
  "assetClassList": ["BILL"],
  "searchQuery": "string",
  "startDate": "2024-07-09T08:58:55.229Z",
  "endDate": "2024-07-09T08:58:55.229Z",
  "securityUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "orderSide": "BUY"
}
```

### Response Body

The response body will be a JSON object containing the following fields:

| Name                                  | Type    | Description                  |
| ------------------------------------- | ------- | ---------------------------- |
| `totalPages`                          | integer | Total number of pages        |
| `totalElements`                       | integer | Total number of elements     |
| `size`                                | integer | Number of elements per page  |
| `content`                             | array   | List of transactions         |
| `content[].id`                        | string  | Transaction UUID             |
| `content[].transactionStatus`         | string  | Status of the transaction    |
| `content[].authStatus`                | string  | Authorization status         |
| `content[].portfolioUUID`             | string  | Portfolio UUID               |
| `content[].portfolioName`             | string  | Portfolio name               |
| `content[].portfolioShortName`        | string  | Portfolio short name         |
| `content[].securityUUID`              | string  | Security UUID                |
| `content[].securityId`                | string  | Security ID                  |
| `content[].bsSecurityMediumId`        | string  | Medium security ID           |
| `content[].bsSecuritySmallId`         | string  | Small security ID            |
| `content[].assetClass`                | string  | Asset class                  |
| `content[].name`                      | string  | Name of the transaction      |
| `content[].isin`                      | string  | ISIN                         |
| `content[].issuer`                    | string  | Issuer                       |
| `content[].executingAccountUUID`      | string  | Executing account UUID       |
| `content[].executingAccount`          | string  | Executing account            |
| `content[].custodianId`               | string  | Custodian ID                 |
| `content[].custodian`                 | string  | Custodian                    |
| `content[].counterParty`              | string  | Counterparty                 |
| `content[].counterPartyUUID`          | string  | Counterparty UUID            |
| `content[].oldTransactionId`          | string  | Old transaction ID           |
| `content[].orderSide`                 | string  | Order side (e.g., BUY, SELL) |
| `content[].quantity`                  | integer | Quantity                     |
| `content[].price`                     | number  | Price                        |
| `content[].consideration`             | number  | Consideration                |
| `content[].considerationWithCurrency` | number  | Consideration with currency  |
| `content[].calculationBase`           | string  | Calculation base             |
| `content[].yield`                     | number  | Yield                        |

### Example Response Body

```json
{
  "totalPages": 0,
  "totalElements": 0,
  "size": 0,
  "content": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "transactionStatus": "AMENDED",
      "authStatus": "APPROVED",
      "portfolioUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "portfolioName": "string",
      "portfolioShortName": "string",
      "securityUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "securityId": "string",
      "bsSecurityMediumId": "string",
      "bsSecuritySmallId": "string",
      "assetClass": "BILL",
      "name": "string",
      "isin": "string",
      "issuer": "string",
      "executingAccountUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "executingAccount": "string",
      "custodianId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "custodian": "string",
      "counterParty": "string",
      "counterPartyUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "oldTransactionId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "orderSide": "BUY",
      "quantity": 0,
      "price": 0,
      "consideration": 0,
      "considerationWithCurrency": 0,
      "calculationBase": "PRICE",
      "yield": 0
    }
  ]
}
```

## Example Code

#### CURL

```bash
curl -X POST "https://api.example.com/api/client/3fa85f64-5717-4562-b3fc-2c963f66afa6/transaction/search" \
-H "Content-Type: application/json" \
-d '{
  "assetClassList": ["BILL"],
  "searchQuery": "string",
  "startDate": "2024-07-09T08:58:55.229Z",
  "endDate": "2024-07-09T08:58:55.229Z",
  "securityUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "orderSide": "BUY",
  "corporateAction": "COUNTER_PARTY_PAYOUT",
  "accountId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "authStatuses": ["APPROVED"],
  "executionStatuses": ["AMENDED"],
  "showSystemGeneratedTransaction": true,
  "brokerTransactionsOnly": true,
  "transactionTypeIds": ["3fa85f64-5717-4562-b3fc-2c963f66afa6"]
}'
```

#### JavaScript (Axios)

```javascript
const axios = require('axios');

const clientId = '3fa85f64-5717-4562-b3fc-2c963f66afa6';
const data = {
  assetClassList: ['BILL'],
  searchQuery: 'string
```
