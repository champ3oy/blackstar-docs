# Get Prices (Performance Chart)

### Endpoint

`POST https://api.uatdev.blackstargroup.ai/swagger-ui/index.html#/Performance/performanceChart`

### Description

This endpoint retrieves prices for securities and can be used to plot performance charts.

You can specify the start and end dates to get prices for a specific period. Include the securityUUID, which you can obtain from the order offer API, in the request body.

### Parameters

| Name      | Type | Location | Required | Description |
| --------- | ---- | -------- | -------- | ----------- |
| startDate | Date | path     | No       | Start Date  |
| endDate   | Date | path     | No       | End Date    |

### Request Body

```json
{
  "securityIdList": ["9dee1f6c-8d9d-45c8-82a0-9c43966bcfaf"],
  "clientIdList": ["9dee1f6c-8d9d-45c8-82a0-9c43966bcfaf"],
  "securityIdList": ["9dee1f6c-8d9d-45c8-82a0-9c43966bcfaf"]
}
```

### Response Example

```json
{
  "clientPerformance": null,
  "portfolioPerformance": null,
  "benchmark": {
    "9dee1e6c-8d9d-45c8-82a0-9c43966bcfaf": [
      {
        "error": false,
        "errorMessage": {},
        "errorRawString": {},
        "securityUUID": "9dee1e6c-8d9d-45c8-82a0-9c43966bcfaf",
        "isin": null,
        "name": "EEBF-Test",
        "securityId": "CIS/EEBF-TEST",
        "bsSecuritySmallId": null,
        "bsSecurityMediumId": "CIS/EEBF-TEST",
        "assetClass": "CIS",
        "fundManager": "Black Star Advisors",
        "fundHouse": null,
        "symbol": "Enhanced Equity Beta Fund Plc",
        "companyName": "Enhanced Equity Beta Fund Plc",
        "issuer": null,
        "securityType": "Equity",
        "sector": null,
        "maturityDate": null,
        "issueDate": "17-06-2024",
        "securityCurrency": {
          "code": "GHS",
          "name": "Ghana Cedi",
          "symbol": "¢",
          "logoKey": "44d87774-b3a7-4b78-869c-415e3c1bbb0a"
        },
        "targetCurrency": null,
        "issuePrice": "1",
        "securityMarket": null,
        "returnRate": null,
        "repoType": null,
        "country": {
          "code": "GH",
          "name": "Ghana",
          "logoKey": "44d87774-b3a7-4b78-869c-415e3c1bbb0a"
        },
        "description": "Dive into the tech-driven future with the first and only Global Tech Equity Fund in Ghana. Investing in global equities with a tech bias, it identifies sectors and companies at the forefront of the 4th Industrial Revolution.",
        "fractionalQuantityAllow": true,
        "logoPath": "country-logo/44d87774-b3a7-4b78-869c-415e3c1bbb0a",
        "tendorNo": null,
        "underlyingSecurityUUID": null,
        "underlyingAssetClass": null,
        "underlyingSecurityId": null,
        "unitPrice": "0.9997",
        "last": "0.9997",
        "cleanPricePercentage": null,
        "dirtyPricePercentage": null,
        "yield": null,
        "timestamp": "03-07-2024",
        "marketQuoteTimestamp": "01-07-2024",
        "aum": null,
        "nav": null,
        "change": "0",
        "changeInValue": "0",
        "changeInYield": null,
        "currency": {
          "code": "GHS",
          "name": "Ghana Cedi",
          "symbol": "¢",
          "logoKey": "44d87774-b3a7-4b78-869c-415e3c1bbb0a"
        },
        "numberOfTrades": null,
        "volumeTraded": null,
        "changeNumberOfTrades": null,
        "changeNumberOfTradesInValue": null,
        "ytdChange": "-0.03",
        "ytdChangeInValue": "-0.0003"
      }
    ]
  }
}
```

In the response, access benchmark.securityUUID, which provides an array of prices. The unitPrice represents the price of the security, and the marketQuoteTimestamp is the closing price on the last available price date.

If timestamp equals marketQuoteTimestamp, the price is considered closed.
If timestamp does not equal marketQuoteTimestamp, the price date is marketQuoteTimestamp.
