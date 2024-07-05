# Order Offer

## Description

The `List Order Offer` API retrieves a list of available order offers for a specific client.

## Endpoint

`POST /api/client/{clientId}/order-offer/search`

## Parameters

| Name        | Type          | Description     | Required | Location |
| ----------- | ------------- | --------------- | -------- | -------- |
| clientId    | string        | Client UUID     | Yes      | Path     |
| portfolioId | string        | Portfolio UUID  | No       | Query    |
| page        | integer       | Current page    | Yes      | Query    |
| size        | integer       | Maximum records | Yes      | Query    |
| sort        | array[string] | Sort order      | No       | Query    |

## Request Body

| Name                        | Type               | Description                             |
| --------------------------- | ------------------ | --------------------------------------- |
| assetClassList              | array[string]      | List of asset classes                   |
| searchQuery                 | string             | Search query                            |
| maturityDate                | string (date-time) | Maturity date in ISO 8601 format        |
| issueDate                   | string (date-time) | Issue date in ISO 8601 format           |
| bondFixedIncomeAssetClasses | array[string]      | List of bond fixed income asset classes |
| currencyCodes               | array[string]      | List of currency codes                  |
| countryNames                | array[string]      | List of country names                   |
| cisTypes                    | array[string]      | List of CIS types                       |
| repoType                    | string             | Type of repo                            |
| productStatus               | array[string]      | List of product statuses                |
| isArchived                  | boolean            | Whether the order is archived           |
| bondBillSectorList          | array[string]      | List of bond bill sectors               |
| onlyWithQuantity            | boolean            | Only include orders with quantity       |
| orderSideOrderOfferList     | array[string]      | List of order side order offers         |
| orderOfferTypes             | array[string]      | List of order offer types               |

## Response

| Name                             | Type               | Description               |
| -------------------------------- | ------------------ | ------------------------- |
| totalElements                    | integer            | Total number of elements  |
| totalPages                       | integer            | Total number of pages     |
| size                             | integer            | Size of the response      |
| content                          | array[object]      | List of order offers      |
| content.error                    | boolean            | Error flag                |
| content.errorMessage             | object             | Error message details     |
| content.errorRawString           | object             | Raw error string          |
| content.securityUUID             | string             | Security UUID             |
| content.isin                     | string             | ISIN of the security      |
| content.name                     | string             | Name of the security      |
| content.securityId               | string             | Security ID               |
| content.bsSecuritySmallId        | string             | Small ID of the security  |
| content.bsSecurityMediumId       | string             | Medium ID of the security |
| content.assetClass               | string             | Asset class               |
| content.fundManager              | string             | Fund manager              |
| content.fundHouse                | string             | Fund house                |
| content.symbol                   | string             | Symbol                    |
| content.companyName              | string             | Company name              |
| content.issuer                   | string             | Issuer                    |
| content.securityType             | string             | Security type             |
| content.sector                   | string             | Sector                    |
| content.maturityDate             | string (date-time) | Maturity date             |
| content.issueDate                | string (date-time) | Issue date                |
| content.securityCurrency         | object             | Security currency details |
| content.securityCurrency.code    | string             | Currency code             |
| content.securityCurrency.name    | string             | Currency name             |
| content.securityCurrency.symbol  | string             | Currency symbol           |
| content.securityCurrency.logoKey | string             | Logo key                  |
| content.targetCurrency           | object             | Target currency details   |
| content.targetCurrency.code      | string             | Currency code             |
| content.targetCurrency.name      | string             | Currency name             |
| content.targetCurrency.symbol    | string             | Currency symbol           |

## Example Request

### JSON Request Body

```json
{
  "assetClassList": ["BILL"],
  "searchQuery": "string",
  "maturityDate": "2024-07-05T12:00:19.416Z",
  "issueDate": "2024-07-05T12:00:19.416Z",
  "bondFixedIncomeAssetClasses": ["CB"],
  "currencyCodes": ["string"],
  "countryNames": ["string"],
  "cisTypes": ["FIXED_INCOME"],
  "repoType": "REPO",
  "productStatus": ["ALL"],
  "isArchived": true,
  "bondBillSectorList": ["MUNICIPAL"],
  "onlyWithQuantity": true,
  "orderSideOrderOfferList": ["BUY"],
  "orderOfferTypes": ["REGULAR"]
}
```

## Example Response

### JSON Response Body

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
      "maturityDate": "2024-07-05T12:00:19.419Z",
      "issueDate": "2024-07-05T12:00:19.419Z",
      "securityCurrency": {
        "code": "string",
        "name": "string",
        "symbol": "string",
        "logoKey": "string"
      },
      "targetCurrency": {
        "code": "string",
        "name": "string",
        "symbol": "string"
      }
    }
  ]
}
```

## Example Code

### CURL

```sh
curl -X POST "https://api.example.com/api/client/{clientId}/order-offer/search?page=0&size=10" \
-H "Content-Type: application/json" \
-d '{
  "assetClassList": ["BILL"],
  "searchQuery": "string",
  "maturityDate": "2024-07-05T12:00:19.416Z",
  "issueDate": "2024-07-05T12:00:19.416Z",
  "bondFixedIncomeAssetClasses": ["CB"],
  "currencyCodes": ["string"],
  "countryNames": ["string"],
  "cisTypes": ["FIXED_INCOME"],
  "repoType": "REPO",
  "productStatus": ["ALL"],
  "isArchived": true,
  "bondBillSectorList": ["MUNICIPAL"],
  "onlyWithQuantity": true,
  "orderSideOrderOfferList": ["BUY"],
  "orderOfferTypes": ["REGULAR"]
}'
```

### JavaScript (Axios)

```javascript
const axios = require("axios");

const data = {
  assetClassList: ["BILL"],
  searchQuery: "string",
  maturityDate: "2024-07-05T12:00:19.416Z",
  issueDate: "2024-07-05T12:00:19.416Z",
  bondFixedIncomeAssetClasses: ["CB"],
  currencyCodes: ["string"],
  countryNames: ["string"],
  cisTypes: ["FIXED_INCOME"],
  repoType: "REPO",
  productStatus: ["ALL"],
  isArchived: true,
  bondBillSectorList: ["MUNICIPAL"],
  onlyWithQuantity: true,
  orderSideOrderOfferList: ["BUY"],
  orderOfferTypes: ["REGULAR"],
};

axios
  .post(
    "https://api.example.com/api/client/{clientId}/order-offer/search?page=0&size=10",
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
    console.error("Error:", error);
  });
```

## Notes

- The `clientId` is a required path parameter and must be provided in the URL.
- The request body must be in JSON format.
- The `page` and `size` query parameters are required to handle pagination.
- The `sort` query parameter is optional and can be used to specify the sort order.
- Date fields such as `maturityDate` and `issueDate` should be in ISO 8601 format.
