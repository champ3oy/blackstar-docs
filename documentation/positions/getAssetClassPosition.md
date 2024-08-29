# Get Positions On All Portfolios

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

#### Example Request

### CURL:

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

### JavaScript (Axios):

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
    "securityUUID": "c3bf3210-a24e-4c7b-a530-4b402504f526",
    "isin": "US5949181045",
    "name": "Microsoft Corporation",
    "securityId": "US.NASDAQ/MSFT",
    "bsSecuritySmallId": null,
    "bsSecurityMediumId": "US.NASDAQ/MSFT",
    "assetClass": "EQUITY",
    "fundManager": null,
    "fundHouse": null,
    "symbol": "MSFT",
    "companyName": "Microsoft Corporation",
    "issuer": null,
    "securityType": "Ordinary",
    "sector": "Technology",
    "maturityDate": null,
    "issueDate": "13-03-1986",
    "securityCurrency": {
      "code": "USD",
      "name": "US Dollar",
      "symbol": "$",
      "logoKey": "32088395-d294-4a67-89bd-39920bab0385"
    },
    "targetCurrency": null,
    "issuePrice": null,
    "securityMarket": "NASDAQ",
    "returnRate": null,
    "repoType": null,
    "fractionalQuantityAllow": true,
    "logoPath": "security-logo/c3bf3210-a24e-4c7b-a530-4b402504f526",
    "portfolioUUID": "8a208c43-a6a3-4abe-9b36-7339c3c68a53",
    "portfolioName": "School Fees",
    "portfolioShortName": "School Fees",
    "quantity": "13.6973684",
    "marketValueOrCurrentValue": "87905.3011446",
    "marketValueOrCurrentValueWithCurrency": "5624.1395486",
    "fxProfitLoss": "17497.494596124",
    "profitLoss": "37116.69323445",
    "profitLossRatio": "73.0807454",
    "avgPrice": "318.9599915",
    "accruedInterest": null,
    "purchaseYield": null,
    "totalCost": "50788.60791015",
    "totalCostWithCurrency": "4368.9125084",
    "profitLossWithCurrency": "1255.2270402",
    "capitalProfitLossWithCurrency": "1255.2270402",  // (Total profit and loss)
    "capitalProfitLossWithCurrencyPercentage": "28.7308807", // (Total profit and loss)
    "nextDividendValueWithCurrency": null,
    "accruedInterestWithCurrency": null,
    "marketYield": null,
    "marketPrice": "410.6000061",
    "fxMarketQuoteLast": "15.63",
    "marketQuoteTimestamp": "28-08-2024",
    "fxMarketQuoteDate": "28-08-2024",
    "marketCleanPricePercentage": null,
    "maturityValue": null,
    "currency": {
      "code": "USD",
      "name": "US Dollar",
      "symbol": "$",
      "logoKey": "32088395-d294-4a67-89bd-39920bab0385"
    },
    "marketCouponRate": null,
    "marketValueOrCurrentValueChangePercentage": "-0.7829089",
    "difference": {
      "capitalProfitLossWithCurrency": "-44.37933938178968", // (1D change)
      "capitalProfitLossWithCurrencyPercentage": "-1.0157983" // (1D change)
    }
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
