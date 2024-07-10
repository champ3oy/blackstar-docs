# Cancel Order API

This API allows you to cancel an existing client order.

## Endpoint

```
POST /api/client/{clientId}/order/{id}/cancel
```

## Description

Cancels a specific order for a given client.

## Parameters

| Name     | Type   | In   | Required | Description |
| -------- | ------ | ---- | -------- | ----------- |
| clientId | string | path | Yes      | Client UUID |
| id       | string | path | Yes      | Order UUID  |

## Request Body

This endpoint does not require a request body.

## Response Body

The response body contains detailed information about the canceled order. Here are some key fields:

- `error`: Boolean indicating if there was an error
- `errorMessage`: Object containing error details (if applicable)
- `id`: UUID of the order
- `clientId`: UUID of the client
- `securityUUID`: UUID of the security
- `orderSide`: Side of the order (BUY/SELL)
- `orderStatus`: Status of the order (e.g., SUBMITTED, CANCELED)
- `quantity`: Order quantity
- `price`: Order price
- `considerationWithCurrency`: Total consideration amount with currency

## Example Response

```json
{
  "error": false,
  "errorMessage": {},
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "clientId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "clientName": "string",
  "clientCode": "string",
  "portfolioId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "portfolioName": "string",
  "securityUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "isin": "string",
  "securityId": "string",
  "orderSide": "BUY",
  "orderStatus": "SUBMITTED",
  "quantity": 0,
  "executedQuantity": 0,
  "remainingQuantity": 0,
  "price": 0,
  "considerationWithCurrency": 0,
  "orderDate": "2024-07-02T10:25:59.584Z",
  "createdOn": "2024-07-02T10:25:59.584Z",
  "updatedOn": "2024-07-02T10:25:59.584Z"
}
```

## Example Request

### cURL

```bash
curl -X POST "https://api.uatdev.blackstargroup.ai/api/client/3fa85f64-5717-4562-b3fc-2c963f66afa6/order/3fa85f64-5717-4562-b3fc-2c963f66afa6/cancel" \
     -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

### JavaScript (Axios)

```javascript
const axios = require("axios");

const clientId = "3fa85f64-5717-4562-b3fc-2c963f66afa6";
const orderId = "3fa85f64-5717-4562-b3fc-2c963f66afa6";

axios
  .post(
    `https://api.uatdev.blackstargroup.ai/api/client/${clientId}/order/${orderId}/cancel`,
    {},
    {
      headers: {
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

## Notes

1. Ensure you have the necessary authentication token before making the API call.
2. The order can only be canceled if it's in a cancellable state (e.g., not fully executed).
3. Once an order is canceled, it cannot be reactivated. A new order must be created if needed.
4. The API returns detailed information about the canceled order, which can be used to verify the cancellation and update local records.
5. If the cancellation fails, check the `error` and `errorMessage` fields in the response for more information.
6. The response includes various details about the security, client, and portfolio associated with the order. This can be useful for reconciliation purposes.

## Error Handling

If an error occurs during the cancellation process, the API will return an error response with details in the `errorMessage` field. Common errors might include:

- Invalid order ID
- Order already canceled
- Order in non-cancellable state
- Insufficient permissions

Always check the `error` field in the response to determine if the cancellation was successful.
