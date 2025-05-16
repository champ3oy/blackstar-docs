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
```

### Notes:

1. Ensure you have the necessary authentication token before making the request.
2. The date parameter should be in the format dd-MM-yyyy.
3. The response includes detailed information about the security position, including market data and performance metrics.
4. Some fields in the response may be null or omitted depending on the security type and available data.
5. Always handle potential errors in your code, as network issues or server problems could occur.
