# Get Client Orders

## Description

This API endpoint retrieves a list of orders for a specific client or portfolio.

## Endpoint

`POST /api/client/{clientId}/order/search`

## Parameters

| Name        | Type    | In    | Required | Description              |
| ----------- | ------- | ----- | -------- | ------------------------ |
| clientId    | string  | path  | Yes      | UUID of the client       |
| portfolioId | string  | query | No       | UUID of the portfolio    |
| page        | integer | query | Yes      | Current page number      |
| size        | integer | query | Yes      | Maximum records per page |

## Request Body

| Name           | Type          | Required | Description                   |
| -------------- | ------------- | -------- | ----------------------------- |
| assetClassList | array[string] | No       | List of asset classes         |
| searchQuery    | string        | No       | Search query                  |
| orderStatuses  | array[string] | No       | List of order statuses        |
| orderSide      | string        | No       | Order side (e.g., BUY, SELL)  |
| startDate      | string        | No       | Start date in ISO 8601 format |
| endDate        | string        | No       | End date in ISO 8601 format   |
| orderType      | string        | No       | Type of order (e.g., MARKET)  |
| orderOfferType | array[string] | No       | List of order offer types     |

## Example Request Body

```json
{
  "assetClassList": ["BILL"],
  "searchQuery": "string",
  "orderStatuses": ["SUBMITTED"],
  "orderSide": "BUY",
  "startDate": "2024-07-02T10:29:46.670Z",
  "endDate": "2024-07-02T10:29:46.670Z",
  "orderType": "MARKET",
  "orderOfferType": ["REGULAR"]
}
```

> `orderStatuses` can be one or more of
> [ SUBMITTED, PENDING, PARTIALLY_FILLED, EXECUTED, REJECTED, CANCELLED, EXPIRED ]

## Responses

### Success (200)

| Name                              | Type    | Description                      |
| --------------------------------- | ------- | -------------------------------- |
| totalElements                     | integer | Total number of elements         |
| totalPages                        | integer | Total number of pages            |
| size                              | integer | Number of records per page       |
| content                           | array   | List of orders                   |
| content[].error                   | boolean | Error status                     |
| content[].errorMessage            | object  | Error message details            |
| content[].errorRawString          | object  | Raw error string details         |
| content[].securityUUID            | string  | Security UUID                    |
| content[].isin                    | string  | ISIN                             |
| content[].name                    | string  | Name                             |
| content[].securityId              | string  | Security ID                      |
| content[].assetClass              | string  | Asset class                      |
| content[].fundManager             | string  | Fund manager                     |
| content[].symbol                  | string  | Symbol                           |
| content[].sector                  | string  | Sector                           |
| content[].maturityDate            | string  | Maturity date in ISO 8601 format |
| content[].securityCurrency        | object  | Security currency details        |
| content[].targetCurrency          | object  | Target currency details          |
| content[].issuePrice              | integer | Issue price                      |
| content[].returnRate              | integer | Return rate                      |
| content[].country                 | object  | Country details                  |
| content[].description             | string  | Description                      |
| content[].fractionalQuantityAllow | boolean | Fractional quantity allowed      |

### Example Response Body

```json
{
  "totalElements": 0,
  "totalPages": 0,
  "size": 0,
  "content": [
    {
      "error": true,
      "errorMessage": {
        "additionalProp1": "string",
        "additionalProp2": "string",
        "additionalProp3": "string"
      },
      "errorRawString": {
        "additionalProp1": "string",
        "additionalProp2": "string",
        "additionalProp3": "string"
      },
      "securityUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "isin": "string",
      "name": "string",
      "securityId": "string",
      "bsSecuritySmallId": "string",
      "bsSecurityMediumId": "string",
      "assetClass": "BILL",
      "fundManager": "string",
      "fundHouse": "string",
      "symbol": "string",
      "companyName": "string",
      "issuer": "string",
      "securityType": "string",
      "sector": "string",
      "maturityDate": "2024-07-02T10:29:46.671Z",
      "issueDate": "2024-07-02T10:29:46.671Z",
      "securityCurrency": {
        "code": "string",
        "name": "string",
        "symbol": "string",
        "logoKey": "string"
      },
      "targetCurrency": {
        "code": "string",
        "name": "string",
        "symbol": "string",
        "logoKey": "string"
      },
      "issuePrice": 0,
      "securityMarket": "string",
      "returnRate": 0,
      "repoType": "REPO",
      "country": {
        "code": "string",
        "name": "string",
        "logoKey": "string"
      },
      "description": "string",
      "fractionalQuantityAllow": true
    }
  ]
}
```

## Example Code

### CURL

```sh
curl -X POST "https://api.uatdev.blackstargroup.ai/api/client/{clientId}/order/search?page=1&size=10" \
-H "Content-Type: application/json" \
-d '{
  "assetClassList": ["BILL"],
  "searchQuery": "string",
  "orderStatuses": ["SUBMITTED"],
  "orderSide": "BUY",
  "startDate": "2024-07-02T10:29:46.670Z",
  "endDate": "2024-07-02T10:29:46.670Z",
  "orderType": "MARKET",
  "orderOfferType": ["REGULAR"]
}'
```

### JavaScript (Axios)

```javascript
const axios = require("axios");

const clientId = "your-client-id";
const page = 1;
const size = 10;

const data = {
  assetClassList: ["BILL"],
  searchQuery: "string",
  orderStatuses: ["SUBMITTED"],
  orderSide: "BUY",
  startDate: "2024-07-02T10:29:46.670Z",
  endDate: "2024-07-02T10:29:46.670Z",
  orderType: "MARKET",
  orderOfferType: ["REGULAR"],
};

axios
  .post(
    `https://api.uatdev.blackstargroup.ai/api/client/${clientId}/order/search?page=${page}&size=${size}`,
    data,
    {
      headers: {
        "Content-Type": "application/json",
      },
    }
  )
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error(error);
  });
```

## Notes

- Ensure the `clientId` is a valid UUID.
- `page` and `size` are required query parameters.
- The request body must be in JSON format.
- Dates should be in ISO 8601 format.
- Optional parameters should be omitted if not needed, as they can filter the search results.
