# Webhooks

## Overview

Webhooks allow your application to receive real-time notifications about specific events that occur within the system. By subscribing to webhooks, you can react to changes or updates without needing to poll the API continuously. This document outlines the supported event types and their payloads.

---

## Supported Event Types

The following event types are supported:

1. **`KYC_STATUS`**
   - Triggered when the status of a submitted KYC is changed.
2. **`ORDER_STATUS`**
   - Triggered when the status of a pending order is changed.
3. **`DEPOSIT_STATUS`**
   - Triggered when a deposit is completed or failed.
4. **`PAYMENT_STATUS`**
   - Triggered when a payment is completed or failed.

---

## Webhook Payload Structure

All webhook payloads follow a consistent structure, with the `event` field specifying the type of event.

---

## Event Details and Payloads

### 1. `KYC_STATUS`

Triggered when the status of a submitted KYC is changed.

#### Example Payload

```json
{
  "eventType": "KYC_STATUS",
  "kycID": "48035e9b-d3dc-46db-90b6-201fa1c1a430",
  "timeStamp": "07-03-2025 09:23",
  "kycStatus": "VERIFIED",
  "rejectionReason": null,
  "clientSubTypeUUID": "8520bcf5-2737-4def-8864-3ff73e878cf2",
  "portfolioId": "25c674d2-159d-4b5d-a965-935e2679678c",
  "clientId": "deafa7a1-d56f-438c-b3a0-ccd7aadc7d32"
}
```

#### Payload Fields

| Field               | Type   | Description                          |
| ------------------- | ------ | ------------------------------------ |
| `eventType`         | string | Event type                           |
| `kycID`             | number | Unique KYC ID.                       |
| `timeStamp`         | string | When this was triggered.             |
| `kycStatus`         | string | Updated status of the KYC.           |
| `rejectionReason`   | string | If KYC was rejected, the reason why. |
| `clientSubTypeUUID` | string | Sub type ID for KYC.                 |
| `portfolioId`       | string | Clients portfolio ID.                |
| `clientId`          | string | Clients ID.                          |

---

### 2. `ORDER_STATUS`

Triggered when the status of a pending order is changed.

#### Example Payload

```json
{
  "eventType": "ORDER_STATUS",
  "timeStamp": "13-03-2025 05:47",
  "clientOrderId": "04ef5a6b-2dc4-4e6d-bc04-df3134099f1e",
  "orderSide": "SELL",
  "clientOrderStatus": "EXECUTED",
  "executedQuantity": 0.0648305,
  "executedConsiderationWithCurrency": 10.0,
  "executedAvgPrice": 154.2483,
  "orderDate": "24-02-2025",
  "clientReference": null
}
```

#### Payload Fields

| Field Name                          | Type        | Example Value                            |
| ----------------------------------- | ----------- | ---------------------------------------- |
| `eventType`                         | string      | `"ORDER_STATUS"`                         |
| `timeStamp`                         | string      | `"13-03-2025 05:47"`                     |
| `clientOrderId`                     | string      | `"04ef5a6b-2dc4-4e6d-bc04-df3134099f1e"` |
| `orderSide`                         | string      | `"SELL"`                                 |
| `clientOrderStatus`                 | string      | `"EXECUTED"`                             |
| `executedQuantity`                  | number      | `0.0648305`                              |
| `executedConsiderationWithCurrency` | number      | `10.0`                                   |
| `executedAvgPrice`                  | number      | `154.2483`                               |
| `orderDate`                         | string      | `"24-02-2025"`                           |
| `clientReference`                   | string/null | `null`                                   |

---

### 3. `DEPOSIT_STATUS`

Triggered when the status of a pending order is changed.

#### Example Payload

```json
{
  "eventType": "DEPOSIT_STATUS",
  "timeStamp": "10-03-2025 12:42",
  "clientReference": "string1258",
  "transactionId": null,
  "amount": 0.1,
  "reasonForFailure": null,
  "status": "FAILED"
}
```

#### Payload Fields

| Field              | Type        | Description          |
| ------------------ | ----------- | -------------------- |
| `eventType`        | string      | `"DEPOSIT_STATUS"`   |
| `timeStamp`        | string      | `"10-03-2025 12:42"` |
| `clientReference`  | string      | `"string1258"`       |
| `transactionId`    | string/null | `null`               |
| `amount`           | number      | `0.1`                |
| `reasonForFailure` | string/null | `null`               |
| `status`           | string      | `"FAILED"`           |

---

### 4. `PAYMENT_STATUS`

Triggered when a payment is completed or failed.

#### Example Payload

```json
{
  "eventType": "PAYMENT_STATUS",
  "status": "SUCCESS",
  "clientReference": "abcdqwerty",
  "transactionCode": "E913465SCOFUX",
  "amount": 1,
  "reasonForFailure": null
}
```

#### Payload Fields

| Field              | Type        | Description        |
| ------------------ | ----------- | ------------------ |
| `eventType`        | string      | `"PAYMENT_STATUS"` |
| `status`           | string      | `"SUCCESS"`        |
| `clientReference`  | string      | `"abcdqwerty"`     |
| `transactionCode`  | string      | `"E913465SCOFUX"`  |
| `amount`           | number      | `1`                |
| `reasonForFailure` | string/null | `null`             |

---

### Explanation of Fields for Each Object

#### `ORDER_STATUS`

- **`eventType`**: Indicates the type of event (`ORDER_STATUS`).
- **`timeStamp`**: The date and time when the event occurred.
- **`clientOrderId`**: A unique identifier for the order.
- **`orderSide`**: Specifies whether the order was a `BUY` or `SELL`.
- **`clientOrderStatus`**: The status of the order (e.g., `EXECUTED`).
- **`executedQuantity`**: The quantity of assets executed in the order.
- **`executedConsiderationWithCurrency`**: The total consideration (cost) of the executed order.
- **`executedAvgPrice`**: The average price at which the order was executed.
- **`orderDate`**: The date when the order was placed.
- **`clientReference`**: A reference ID provided by the client (if applicable).

#### `DEPOSIT_STATUS`

- **`eventType`**: Indicates the type of event (`DEPOSIT_STATUS`).
- **`timeStamp`**: The date and time when the event occurred.
- **`clientReference`**: A reference ID provided by the client for tracking purposes.
- **`transactionId`**: A unique identifier for the transaction (if applicable).
- **`amount`**: The amount involved in the deposit.
- **`reasonForFailure`**: A description of why the deposit failed (if applicable).
- **`status`**: The status of the deposit (e.g., `FAILED`).

#### `PAYMENT_STATUS`

- **`eventType`**: Indicates the type of event (`PAYMENT_STATUS`).
- **`status`**: The status of the payment (e.g., `SUCCESS`).
- **`clientReference`**: A reference ID provided by the client for tracking purposes.
- **`transactionCode`**: A unique code associated with the payment transaction.
- **`amount`**: The amount involved in the payment.
- **`reasonForFailure`**: A description of why the payment failed (if applicable).

---

## Handling Webhooks

To handle webhooks, your server should:

1. Expose an endpoint (e.g., `/webhook`) to receive POST requests.
2. Verify the authenticity of the request (e.g., using a shared secret or signature).
3. Parse the payload and take appropriate actions based on the `event` type.
