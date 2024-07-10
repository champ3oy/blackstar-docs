# Get Position for Security

### Endpoint

`POST /api/client/{clientId}/product/{securityId}/position`

### Description

This endpoint retrieves the position for a selected security in a client's portfolio.

### Parameters

| Name           | Type                 | Location | Required | Description                                                              |
| -------------- | -------------------- | -------- | -------- | ------------------------------------------------------------------------ |
| clientId       | string ($uuid)       | path     | Yes      | Client UUID                                                              |
| securityId     | string ($uuid)       | path     | Yes      | Security UUID                                                            |
| portfolioId    | string ($uuid)       | query    | Yes      | Portfolio UUID                                                           |
| counterPartyId | string ($uuid)       | query    | No       | Counter Party UUID                                                       |
| custodianId    | string ($uuid)       | query    | No       | Custodian UUID                                                           |
| date           | string ($dd-MM-yyyy) | query    | No       | Date for which to fetch position. If not provided, today's date is used. |

### Request Body

This endpoint doesn't require a request body.

### Response Body

The response is a JSON object containing detailed information about the security position. It includes fields such as:

- Security details (UUID, ISIN, name, asset class, etc.)
- Portfolio details
- Counterparty and custodian information
- Quantity and value details
- Profit/loss information
- Currency details
- Market data (price, yield, etc.)

For a full list of fields, refer to the example response below.

### Example Request

### CURL:

```bash
curl -X POST "https://api.uatdev.blackstargroup.ai/api/client/123e4567-e89b-12d3-a456-426614174000/product/98765432-e89b-12d3-a456-426614174000/position?portfolioId=abcdef12-e89b-12d3-a456-426614174000&date=13-01-2020" \
     -H "Accept: application/json" \
     -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

### JavaScript (Axios):

```javascript
const axios = require("axios");

axios
  .post(
    "https://api.uatdev.blackstargroup.ai/api/client/123e4567-e89b-12d3-a456-426614174000/product/98765432-e89b-12d3-a456-426614174000/position",
    null,
    {
      params: {
        portfolioId: "abcdef12-e89b-12d3-a456-426614174000",
        date: "13-01-2020",
      },
      headers: {
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

### Example Response:

```json
{
  "error": false,
  "errorMessage": {},
  "errorRawString": {},
  "securityUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "isin": "US0378331005",
  "name": "Apple Inc.",
  "securityId": "AAPL",
  "assetClass": "EQUITY",
  "fundManager": "N/A",
  "fundHouse": "N/A",
  "symbol": "AAPL",
  "companyName": "Apple Inc.",
  "issuer": "Apple Inc.",
  "securityType": "Common Stock",
  "sector": "Technology",
  "maturityDate": null,
  "issueDate": "1980-12-12T00:00:00Z",
  "securityCurrency": {
    "code": "USD",
    "name": "US Dollar",
    "symbol": "$"
  },
  "quantity": 100,
  "marketValue": 15000,
  "currentValue": 15000,
  "marketValueOrCurrentValue": 15000,
  "fxProfitLoss": 0,
  "profitLoss": 2000,
  "profitLossRatio": 0.1538,
  "avgPrice": 130,
  "marketPrice": 150,
  "marketQuoteTimestamp": "2024-07-02T10:53:49.087Z",
  "portfolioUUID": "abcdef12-e89b-12d3-a456-426614174000",
  "portfolioName": "Tech Growth Portfolio"
}
```

### Notes:

1. Ensure you have the necessary authentication token before making the request.
2. The date parameter should be in the format dd-MM-yyyy.
3. The response includes detailed information about the security position, including market data and performance metrics.
4. Some fields in the response may be null or omitted depending on the security type and available data.
5. Always handle potential errors in your code, as network issues or server problems could occur.
