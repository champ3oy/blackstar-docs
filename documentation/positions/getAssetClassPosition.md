# Get Positions based on different asset classes

### Endpoint

`POST /api/client/{clientId}/position`

### Description

This endpoint retrieves positions for a client or portfolio based on various criteria, including asset classes, search queries, and date ranges.

### Parameters

| Name        | Type                 | Location | Required | Description                                                               |
| ----------- | -------------------- | -------- | -------- | ------------------------------------------------------------------------- |
| clientId    | string ($uuid)       | path     | Yes      | Client UUID                                                               |
| portfolioId | string ($uuid)       | query    | No       | Portfolio UUID                                                            |
| securityId  | string ($uuid)       | query    | No       | Security UUID                                                             |
| date        | string ($dd-MM-yyyy) | query    | No       | Date for which to fetch positions. If not provided, today's date is used. |

### Request Body

The request body is a JSON object with the following properties:

```json
{
  "assetClassList": ["BILL"],
  "searchQuery": "string",
  "maturityDate": "2024-07-02T10:57:55.901Z",
  "issueDate": "2024-07-02T10:57:55.901Z",
  "bondFixedIncomeAssetClasses": ["CB"],
  "currencyCodes": ["string"],
  "countryNames": ["string"],
  "cisTypes": ["FIXED_INCOME"],
  "repoType": "REPO",
  "productStatus": ["ALL"],
  "isArchived": true,
  "bondBillSectorList": ["MUNICIPAL"]
}
```

### Response Body

The response is an array of JSON objects, each representing a position. Each object contains detailed information about the security, including:

- Security details (UUID, ISIN, name, asset class, etc.)
- Portfolio and counterparty information
- Quantity and value details
- Profit/loss information
- Market data (price, yield, etc.)
- Currency information

### Example Request

CURL:

```bash
curl -X POST "https://api.uatdev.blackstargroup.ai/api/client/123e4567-e89b-12d3-a456-426614174000/position?portfolioId=abcdef12-e89b-12d3-a456-426614174000&date=13-01-2020" \
     -H "Content-Type: application/json" \
     -H "Accept: application/json" \
     -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
     -d '{
  "assetClassList": ["BILL"],
  "searchQuery": "Treasury",
  "maturityDate": "2025-12-31T00:00:00Z",
  "issueDate": "2020-01-01T00:00:00Z",
  "bondFixedIncomeAssetClasses": ["CB"],
  "currencyCodes": ["USD"],
  "countryNames": ["United States"],
  "cisTypes": ["FIXED_INCOME"],
  "repoType": "REPO",
  "productStatus": ["ALL"],
  "isArchived": false,
  "bondBillSectorList": ["GOVERNMENT"]
}'
```

JavaScript (Axios):

```javascript
const axios = require("axios");

const data = {
  assetClassList: ["BILL"],
  searchQuery: "Treasury",
  maturityDate: "2025-12-31T00:00:00Z",
  issueDate: "2020-01-01T00:00:00Z",
  bondFixedIncomeAssetClasses: ["CB"],
  currencyCodes: ["USD"],
  countryNames: ["United States"],
  cisTypes: ["FIXED_INCOME"],
  repoType: "REPO",
  productStatus: ["ALL"],
  isArchived: false,
  bondBillSectorList: ["GOVERNMENT"],
};

axios
  .post(
    "https://api.uatdev.blackstargroup.ai/api/client/123e4567-e89b-12d3-a456-426614174000/position",
    data,
    {
      params: {
        portfolioId: "abcdef12-e89b-12d3-a456-426614174000",
        date: "13-01-2020",
      },
      headers: {
        "Content-Type": "application/json",
        Accept: "application/json",
        Authorization: "Bearer YOUR_ACCESS_TOKEN",
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

### Example Response

```json
[
  {
    "securityUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "isin": "US912796XA78",
    "name": "US Treasury Bill",
    "securityId": "T-BILL-3M",
    "assetClass": "BILL",
    "securityType": "Treasury Bill",
    "sector": "Government",
    "maturityDate": "2025-12-31T00:00:00Z",
    "issueDate": "2020-01-01T00:00:00Z",
    "securityCurrency": {
      "code": "USD",
      "name": "US Dollar",
      "symbol": "$"
    },
    "country": {
      "code": "US",
      "name": "United States"
    },
    "quantity": 1000000,
    "marketValue": 998500,
    "currentValue": 998500,
    "marketPrice": 99.85,
    "marketYield": 0.015,
    "profitLoss": -1500,
    "profitLossRatio": -0.0015
  }
]
```

### Notes

1. Ensure you have the necessary authentication token before making the request.
2. The date parameter should be in the format dd-MM-yyyy.
3. The response includes detailed information about each position matching the specified criteria.
4. Some fields in the response may be null or omitted depending on the security type and available data.
5. The assetClassList and other filter parameters in the request body allow for fine-grained control over the returned positions.
6. Always handle potential errors in your code, as network issues or server problems could occur.
