# Create Order Request

## Description

This API takes a [Hubtel](https://hubtel.com) payment reference, in addition to the `request body` to create an order for the client.

> **_Important Notice!_**
> To use this API, please contect us for the [Hubtel](https://hubtel.com) branch API keys you need to use for payment collection.

## Endpoint

`POST /api/client/{clientId}/portfolio/{portfolioId}/collectionRequest/v1/create`

---

## Parameters

| Name        | Type   | In   | Description    |
| ----------- | ------ | ---- | -------------- |
| clientId    | string | path | Client UUID    |
| portfolioId | string | path | Portfolio UUID |

---

## Request Body

| Name            | Type   | Description                | Required |
| --------------- | ------ | -------------------------- | -------- |
| amount          | number | The amount to be collected | Yes      |
| successUrl      | string | URL to redirect on success | No       |
| failUrl         | string | URL to redirect on failure | No       |
| securityId      | string | Security UUID              | Yes      |
| orderOfferId    | string | Order offer UUID           | No       |
| clientReference | string | Hubtel reference string    | Yes      |

#### Example Request Body

```json
{
  "amount": 1000,
  "successUrl": "https://example.com/success",
  "failUrl": "https://example.com/failure",
  "securityId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "orderOfferId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "clientReference": "order123"
}
```

---

## Response

| Name                  | Type   | Description                      |
| --------------------- | ------ | -------------------------------- |
| id                    | string | Collection request UUID          |
| portfolioId           | string | Portfolio UUID                   |
| portfolioName         | string | Portfolio name                   |
| hubtleConfigId        | string | Hubtle configuration UUID        |
| amount                | number | Amount to be collected           |
| transactionId         | string | Transaction UUID                 |
| requestType           | string | Type of request                  |
| status                | string | Status of the request            |
| executionErrorMessage | string | Error message if execution fails |
| description           | string | Description of the request       |
| valueDate             | string | Value date of the transaction    |
| custodianId           | string | Custodian UUID                   |

#### Example Response Body

```json
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "portfolioId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "portfolioName": "Sample Portfolio",
  "hubtleConfigId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "amount": 1000,
  "transactionId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "requestType": "ONLINE_CHECKOUT_COLLECTION",
  "status": "SUBMITTED",
  "executionErrorMessage": "",
  "description": "Collection for order123",
  "valueDate": "2024-07-09T08:46:45.543Z",
  "custodianId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

---

## Example Code

#### CURL

```sh
curl -X POST "https://api.example.com/api/client/3fa85f64-5717-4562-b3fc-2c963f66afa6/portfolio/3fa85f64-5717-4562-b3fc-2c963f66afa6/collectionRequest/v1/create" \
-H "Content-Type: application/json" \
-d '{
  "amount": 1000,
  "successUrl": "https://example.com/success",
  "failUrl": "https://example.com/failure",
  "securityId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "orderOfferId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "clientReference": "order123"
}'
```

#### JavaScript (Axios)

```javascript
const axios = require("axios");

const data = {
  amount: 1000,
  successUrl: "https://example.com/success",
  failUrl: "https://example.com/failure",
  securityId: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  orderOfferId: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  clientReference: "order123",
};

axios
  .post(
    "https://api.example.com/api/client/3fa85f64-5717-4562-b3fc-2c963f66afa6/portfolio/3fa85f64-5717-4562-b3fc-2c963f66afa6/collectionRequest/v1/create",
    data
  )
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error(error);
  });
```

---

## Notes

- The `clientId` and `portfolioId` parameters must be valid UUIDs.
- The `amount` should be a positive number.
- The `successUrl` and `failUrl` must be valid URLs.
- The `securityId` and `orderOfferId` should be valid UUIDs.
- The `clientReference` must be the hubtel reference string for the payment.
