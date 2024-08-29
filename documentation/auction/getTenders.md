# Order Offer

## Description

The `List Order Offer` API retrieves a list of available tenders for auction

## Endpoint

`POST /api/client/{clientId}/order-offer/search`

## Parameters

| Name        | Type          | Description     | Required | Location |
| ----------- | ------------- | --------------- | -------- | -------- |
| clientId    | string        | Client UUID     | Yes      | Path     |
| page        | integer       | Current page, starts from 0    | Yes      | Query    |
| size        | integer       | Maximum records | Yes      | Query    |

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

## Response

| Column Name                                   | Data Type      | Description                                                        |
|-----------------------------------------------|----------------|--------------------------------------------------------------------|
| `securityUUID`                                | string         | Security identifier for the security                   |
| `description`                                 | string         | A description of the security                                      |
| `logoPath`                                    | string | Path to the logo of the security                                   |
| `id`                                          | string         | Unique identifier for the security                          |
| `orderSide`                                   | string  | Side of the order, "BUY" or "SELL                          |
| `currency`                                    | string  | Currency code, "GHS"                                         |
| `securityName`                                | string | Name of the security                                               |
| `minOrderAmount`                              | integer | Minimum order amount for non competitive bids                                               |
| `minOrderAmountForCompetitivePrimaryAuction`  | integer | Minimum order amount for competitive bids               |
| `minYield`                                    | integer | Minimum yield                                       |
| `maxYield`                                    | integer | Maximum yield                                       |
| `prevYield`                                   | integer | Previous yield value                                              |
| `primaryAuctionType`                          | string  | Type of the primary auction, "BOTH", "COMPETITIVE", "NON_COMPETITIVE".     |


### JSON Response Body

```json
{
  "totalElements": 0,
  "totalPages": 0,
  "size": 0,
  "content": [
    {
      "securityUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "description": "string",
      "logoPath": "country-logo/44d87774-b3a7-4b78-869c-415e3c1bbb0a",
      "id": "6d64867d-5cfd-45b1-829a-a510b12396aaa",
      "orderSide": "BUY",
      "currency": "GHS",
      "securityName": "182 Day GHS T-bill",
      "minOrderAmount": "100",
      "minOrderAmountForCompetitivePrimaryAuction": "500000",
      "minYield": null,
      "maxYield": null,
      "prevYield": "26.6854",
      "primaryAuctionType": "COMPETITIVE"
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
