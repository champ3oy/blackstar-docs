# Order Offer

## Description

The `List Order Offer` API retrieves a list of available tenders for auction

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
| assetClassList              | array[string]      | This should be an array of "BILL"       |
| orderOfferTypes             | array[string]      | This should be an array of "PRIMARY_AUCTION"               |

## Example Request

### JSON Request Body

```json
{
  "assetClassList": ["BILL"],
  "orderOfferTypes": ["PRIMARY_AUCTION"]
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
      "securityUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "isin": "string",
      "name": "string",
      "securityId": "string",
      "bsSecuritySmallId": "string",
      "bsSecurityMediumId": "string",
      "assetClass": "BILL",
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
      },
      "description": "string",
    "logoPath": "country-logo/44d87774-b3a7-4b78-869c-415e3c1bbb0a",
    "tendorNo": "1918",
    "id": "6d64867d-5cfd-45b1-829a-a510b12396aaa",
    "offerStartDate": "26-08-2024",
    "offerEndDate": "30-08-2024",
    "source": "BSB",
    "quantity": null,
    "orderSide": "BUY",
    "orderOfferType": "PRIMARY_AUCTION",
    "currency": null,
    "tenor": "182",
    "orderOfferStartTime": null,
    "orderOfferEndTime": "11:00",
    "securityName": "182 Day GHS T-bill",
    "companyNameOrIssuer": "Treasury Bill",
    "unitPriceOrYield": null,
    "unitPriceOrYieldChange": null,
    "unitPriceOrYieldChangePercentage": null,
    "minOrderAmount": "100",
    "minOrderAmountForCompetitivePrimaryAuction": "500000",
    "minYield": null,
    "maxYield": null,
    "minDiscountRate": null,
    "maxDiscountRate": null,
    "prevYield": "26.6854",
    "primaryAuctionType": "BOTH"
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
  "orderOfferTypes": ["PRIMARY_AUCTION"]
}'
```

### JavaScript (Axios)

```javascript
const axios = require("axios");

const data = {
  assetClassList: ["BILL"],
  orderOfferTypes: ["PRIMARY_AUCTION"],
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
