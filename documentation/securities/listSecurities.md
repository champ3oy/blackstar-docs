# List Available Securities

## Description

This API endpoint retrieves available securities/products based on specified search criteria.

## Endpoint

- **URL:** `/api/product/search`
- **Method:** POST
- **Description:** Get available securities/products.

## Parameters

| Name | Type    | In    | Required | Description               |
| ---- | ------- | ----- | -------- | ------------------------- |
| page | integer | query | Yes      | Current page number.      |
| size | integer | query | Yes      | Maximum records per page. |

## Request Body

The request body must be in JSON format.

### Schema

| Field                       | Type    | Required | Description                                |
| --------------------------- | ------- | -------- | ------------------------------------------ |
| assetClassList              | array   | No       | List of asset classes to filter by.        |
| searchQuery                 | string  | No       | Query string for searching products.       |
| maturityDate                | string  | No       | Filter by maturity date (ISO 8601 format). |
| issueDate                   | string  | No       | Filter by issue date (ISO 8601 format).    |
| bondFixedIncomeAssetClasses | array   | No       | List of bond fixed income asset classes.   |
| currencyCodes               | array   | No       | List of currency codes to filter by.       |
| countryNames                | array   | No       | List of country names to filter by.        |
| cisTypes                    | array   | No       | List of CIS types to filter by.            |
| repoType                    | string  | No       | Type of repo to filter by.                 |
| productStatus               | array   | No       | List of product statuses to filter by.     |
| isArchived                  | boolean | No       | Filter by archived status.                 |
| bondBillSectorList          | array   | No       | List of bond bill sectors to filter by.    |

### Example Request Body

```json
{
  "assetClassList": ["BILL"],
  "searchQuery": "string",
  "maturityDate": "2024-07-09T10:31:48.362Z",
  "issueDate": "2024-07-09T10:31:48.362Z",
  "bondFixedIncomeAssetClasses": ["CB"],
  "currencyCodes": ["USD"],
  "countryNames": ["USA"],
  "cisTypes": ["FIXED_INCOME"],
  "repoType": "REPO",
  "productStatus": ["ALL"],
  "isArchived": true,
  "bondBillSectorList": ["MUNICIPAL"]
}
```

## Response

### Response Body

The response body will be in JSON format.

| Field                         | Type    | Description                              |
| ----------------------------- | ------- | ---------------------------------------- |
| totalPages                    | integer | Total number of pages.                   |
| totalElements                 | integer | Total number of elements.                |
| size                          | integer | Number of records per page.              |
| content                       | array   | List of products matching the query.     |
| content.error                 | boolean | Indicates if there was an error.         |
| content.errorMessage          | object  | Details of the error message.            |
| content.errorRawString        | object  | Raw error message details.               |
| content.securityUUID          | string  | Security UUID.                           |
| content.isin                  | string  | ISIN of the product.                     |
| content.name                  | string  | Name of the product.                     |
| content.securityId            | string  | Security ID.                             |
| content.bsSecurityMediumId    | string  | BS Security Medium ID.                   |
| content.assetClass            | string  | Asset class of the product.              |
| content.issuer                | string  | Issuer of the product.                   |
| content.issueDate             | string  | Issue date of the product (ISO 8601).    |
| content.maturityDate          | string  | Maturity date of the product (ISO 8601). |
| content.coupon                | number  | Coupon rate of the product.              |
| content.baseCurrency          | string  | Base currency of the product.            |
| content.targetCurrency        | string  | Target currency of the product.          |
| content.fundManager           | string  | Fund manager of the product.             |
| content.symbol                | string  | Symbol of the product.                   |
| content.companyName           | string  | Company name.                            |
| content.tenor                 | string  | Tenor of the product.                    |
| content.returnRate            | number  | Return rate of the product.              |
| content.underlyingAsset       | string  | Underlying asset.                        |
| content.underlyingAssetUUID   | string  | Underlying asset UUID.                   |
| content.yield                 | number  | Yield of the product.                    |
| content.country               | string  | Country of the product.                  |
| content.market                | string  | Market of the product.                   |
| content.fixedIncomeClass      | string  | Fixed income class.                      |
| content.issueType             | string  | Issue type of the product.               |
| content.issueAmount           | number  | Issue amount.                            |
| content.issuerIndustry        | string  | Issuer industry.                         |
| content.announcementDate      | string  | Announcement date (ISO 8601).            |
| content.couponType            | string  | Coupon type.                             |
| content.annualCouponFrequency | number  | Annual coupon frequency.                 |
| content.firstCouponDate       | string  | First coupon date (ISO 8601).            |
| content.sellYield             | number  | Sell yield.                              |
| content.repoType              | string  | Repo type.                               |
| content.dayCountBasis         | string  | Day count basis.                         |
| content.couponDateBasis       | string  | Coupon date basis.                       |

### Example Response Body

```json
{
  "totalPages": 0,
  "totalElements": 0,
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
      "bsSecurityMediumId": "string",
      "assetClass": "BILL",
      "issuer": "string",
      "issueDate": "2024-07-09T10:31:48.407Z",
      "maturityDate": "2024-07-09T10:31:48.407Z",
      "coupon": 0,
      "baseCurrency": "string",
      "targetCurrency": "string",
      "fundManager": "string",
      "symbol": "string",
      "companyName": "string",
      "tenor": "string",
      "returnRate": 0,
      "underlyingAsset": "string",
      "underlyingAssetUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "yield": 0,
      "country": "string",
      "market": "string",
      "fixedIncomeClass": "string",
      "issueType": "string",
      "issueAmount": 0,
      "issuerIndustry": "string",
      "announcementDate": "2024-07-09T10:31:48.407Z",
      "couponType": "string",
      "annualCouponFrequency": 0,
      "firstCouponDate": "2024-07-09T10:31:48.407Z",
      "sellYield": 0,
      "repoType": "REPO",
      "dayCountBasis": "ACTUAL_360",
      "couponDateBasis": "DAY"
    }
  ]
}
```

## Example Code

#### cURL

```sh
curl -X POST "https://api.example.com/api/product/search?page=1&size=10" -H "accept: application/json" -H "Content-Type: application/json" -d '{
  "assetClassList": ["BILL"],
  "searchQuery": "string",
  "maturityDate": "2024-07-09T10:31:48.362Z",
  "issueDate": "2024-07-09T10:31:48.362Z",
  "bondFixedIncomeAssetClasses": ["CB"],
  "currencyCodes": ["USD"],
  "countryNames": ["USA"],
  "cisTypes": ["FIXED_INCOME"],
  "repoType": "REPO",
  "productStatus": ["ALL"],
  "isArchived": true,
  "bondBillSectorList": ["MUNICIPAL"]
}'
```

#### JavaScript (Axios)

```javascript
const axios = require('axios');

const data = {
  assetClassList: ["BILL"],
  searchQuery: "string",
  maturityDate: "2024-07-09T10:31:48.362Z",
  issueDate: "2024-07-09T10:31:48.362Z",
  bondFixedIncomeAssetClasses: ["CB"],
  currencyCodes: ["USD"],
  countryNames: ["USA"],
  cisTypes:
```
