# Create Client Order

This endpoint allows you to create an order for a client within a specific portfolio.

> **New** 📢
> You can now add a webhook for order status updates
> When an order is created, you can include a webhook URL in the request body

## Endpoint Details

```
POST /api/client/{clientId}/portfolio/{portfolioId}/order/v1/place
```

## Request

### Parameters

| Name        | Type          | Location | Required | Description                            |
| ----------- | ------------- | -------- | -------- | -------------------------------------- |
| clientId    | string (UUID) | path     | Yes      | The unique identifier of the client    |
| portfolioId | string (UUID) | path     | Yes      | The unique identifier of the portfolio |

### Request Body

| Field                          | Type          | Required              | Description                                                 |
| ------------------------------ | ------------- | --------------------- | ----------------------------------------------------------- |
| securityUUID                   | string (UUID) | Yes                   | Unique identifier of the security                           |
| orderSide                      | string        | Yes                   | Side of the order (e.g., "BUY" or "SELL")                   |
| orderType                      | string        | Yes                   | Type of order (e.g., "MARKET" or "LIMIT")                   |
| sendToBank                     | boolean       | Yes (for SELL orders) | Should be `true` at all times                               |
| quantity                       | number        | No                    | Quantity of securities to order                             |
| price                          | number        | No                    | Price per security (required for limit orders)              |
| yield                          | number        | No                    | Yield of the security                                       |
| considerationWithCurrency      | number        | No                    | Consideration amount including currency                     |
| totalConsiderationWithCurrency | number        | No                    | Total consideration amount including currency               |
| description                    | string        | No                    | Additional description for the order                        |
| counterPartyUUID               | string (UUID) | No                    | Unique identifier of the counterparty                       |
| settlementType                 | string        | No                    | Type of settlement (e.g., "T0", "T+1", "T+2")               |
| orderValidity                  | string        | No                    | Validity of the order (e.g., "GTC" for Good Till Cancelled) |
| orderOfferId                   | string (UUID) | No                    | Unique identifier of the order offer                        |
| primaryAuctionType             | string        | No                    | Type of primary auction (e.g., "COMPETITIVE")               |
| consideration                  | number        | No                    | Consideration amount                                        |
| totalConsideration             | number        | No                    | Total consideration amount                                  |
| currency                       | string        | No                    | Currency code                                               |
| clientReference                | string        | No                    | Client's payment reference                                  |
| webhookUrl                     | string        | No                    | Client's payment reference                                  |

## Response

### Success Response (200 OK)

Content-Type: application/json

The response body includes detailed information about the created order, including client details, security information, order status, and execution details.

Key fields in the response:

- `id`: Unique identifier of the created order
- `clientOrderStatus`: Status of the client order (e.g., "SUBMITTED")
- `executedQuantity`: Quantity of securities executed
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
  "clientReference": "string",
  "securityName": "string",
  "companyNameOrIssuer": "string",
  "cancellable": true
}
```

### Webhook Data

```json
{
  "eventType": "PAYMENT_STATUS",
  "status": "SUCCESS",
  "clientReference": "abcdqwerty",
  "transactionCode": "zxcvbnmqwerty",
  "amount": 1,
  "reasonForFailure": null
}
```

Additionally, kindly make sure to whitelist our production IP (18.102.87.24) on the API receiving the webhook. This will ensure that only we can send messages to the webhook, and no one else can push messages to it.

Once the payment is completed, we will send an immediate webhook response.
If the first attempt fails, the first retry will occur after 5-10 minutes, followed by a second retry after another 5-10 minutes.
In total, we will attempt three retries.

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
  "orderType": "MARKET",
  "quantity": 100,
  "price": 50.25,
  "sendToBank": true,
  "yield": 2.5,
  "considerationWithCurrency": 5025,
  "description": "Market order for 100 shares",
  "settlementType": "T+2",
  "orderValidity": "GTC"
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
  orderType: "MARKET",
  quantity: 100,
  sendToBank: true,
  price: 50.25,
  yield: 2.5,
  considerationWithCurrency: 5025,
  description: "Market order for 100 shares",
  settlementType: "T+2",
  orderValidity: "GTC",
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
