# Create Client Order

## Endpoint

```
POST /api/client/{clientId}/portfolio/{portfolioId}/order/place
```

## Description

This endpoint allows you to create an order for a client within a specific portfolio. For auctions, 

## Parameters

| Name        | Type          | Location | Required | Description                            |
| ----------- | ------------- | -------- | -------- | -------------------------------------- |
| clientId    | string (UUID) | path     | Yes      | The unique identifier of the client    |
| portfolioId | string (UUID) | path     | Yes      | The unique identifier of the portfolio |

## Request Body

Content-Type: application/json

| Field                          | Type          | Required | Description                                                 |
| ------------------------------ | ------------- | -------- | ----------------------------------------------------------- |
| securityUUID                   | string (UUID) | Yes      | Unique identifier of the security                           |
| orderSide                      | string        | Yes      | Side of the order (should always be "BUY")                   |
| yield                          | number        | Yes (for COMPETITIVE)       | Yield of the security                                       |
| consideration      | number        | Yes       | Consideration amount                    |
| orderOfferId                   | string (UUID) | Yes       | ID from the order offer request                        |
| primaryAuctionType             | string        | Yes       | Type of primary auction (e.g., "COMPETITIVE")               |

## Response

### Success Response (200 OK)

Content-Type: application/json

The response body includes detailed information about the created order, including client details, security information, order status, and execution details.

Key fields in the response:

- `id`: Unique identifier of the created order
- `clientOrderStatus`: Status of the client order (e.g., "SUBMITTED")
- `executedQuantity`: Maturity amount of executed security
- `executedConsiderationWithCurrency`: Executed consideration amount including currency
- `executedAvgPrice`: Average execution price
- `executedAvgYield`: Average execution yield

### Response Body Example

```json
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
  "maturityDate": "2024-07-02T10:20:56.211Z",
  "issueDate": "2024-07-02T10:20:56.211Z",
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
  "fractionalQuantityAllow": true,
  "logoPath": "string",
  "tendorNo": "string",
  "underlyingSecurityUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "underlyingAssetClass": "BILL",
  "underlyingSecurityId": "string",
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "clientId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "clientName": "string",
  "clientCode": "string",
  "clientTypeName": "string",
  "clientSubTypeName": "string",
  "portfolioId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "portfolioName": "string",
  "portfolioShortName": "string",
  "portfolioCode": 0,
  "orderSide": "BUY",
  "settlementType": "T0",
  "orderValidity": "GTC",
  "orderType": "MARKET",
  "clientOrderStatus": "SUBMITTED",
  "quantity": 0,
  "executedQuantity": 0,
  "remainingQuantity": 0,
  "executedConsiderationWithCurrency": 0,
  "price": 0,
  "yield": 0,
  "cleanPricePercentage": 0,
  "considerationWithCurrency": 0,
  "executedAvgPrice": 0,
  "executedAvgYield": 0,
  "executedAvgCleanPricePercentage": 0,
  "pickedBy": "string",
  "offerActivateOn": "2024-07-02T10:20:56.211Z",
  "offerExpireOn": "2024-07-02T10:20:56.211Z",
  "counterPartyUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "counterPartyName": "string",
  "counterPartyAlias": "string",
  "orderDate": "2024-07-02T10:20:56.211Z",
  "managedSecurity": true,
  "securityName": "string",
  "companyNameOrIssuer": "string",
  "cancellable": true
}
```

### Error Response

In case of an error, the response will include:

- error: Boolean indicating if an error occurred
- errorMessage: Object containing error messages
- errorRawString: Object containing raw error strings

## Example Usage

### cURL

```bash
curl -X POST "https://api.uatdev.blackstargroup.ai/api/client/123e4567-e89b-12d3-a456-426614174000/portfolio/98765432-e89b-12d3-a456-426614174000/order/place" \
     -H "Content-Type: application/json" \
     -d '{
  "securityUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "orderSide": "BUY",
  "quantity": 100,
  "price": 50.25,
  "yield": 2.5,
  "consideration": 5025,
  "orderOfferId": "3fa85f64-5717-4562-b3fc-2c963f66a1234"
}'
```

### JavaScript (Axios)

```javascript
const axios = require("axios");

const clientId = "123e4567-e89b-12d3-a456-426614174000";
const portfolioId = "98765432-e89b-12d3-a456-426614174000";

const orderData = {
  securityUUID: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  orderSide: "BUY",
  quantity: 100,
  price: 50.25,
  yield: 2.5,
  consideration: 5025,
  orderOfferId: "3fa85f64-5717-4562-b3fc-2c963f66a1234"
};

axios
  .post(
    `https://api.uatdev.blackstargroup.ai/api/client/${clientId}/portfolio/${portfolioId}/order/place`,
    orderData,
    {
      headers: {
        "Content-Type": "application/json",
      },
    }
  )
  .then((response) => {
    console.log("Order placed successfully:", response.data);
  })
  .catch((error) => {
    console.error("Error placing order:", error.response.data);
  });
```

## Notes

1. Ensure that you have the necessary authentication and authorization to access this endpoint.
2. The `clientId` and `portfolioId` in the URL path are crucial for identifying the correct client and portfolio for the order.
3. The `orderType` field determines which other fields are required. For example, a "MARKET" order may not require a `price`, while a "LIMIT" order would.
4. The `orderSide` field should be either "BUY" or "SELL".
5. Be cautious with the `buyAllOrSellAll` flag, as it may affect the entire portfolio position.
6. The response includes detailed information about the order and its execution status. Monitor the `clientOrderStatus` field for the current state of the order.
7. Error handling is important. Always check the `error` field in the response to determine if the order was placed successfully.
8. The API supports various settlement types and order validities. Ensure you use the appropriate values based on your trading requirements.
