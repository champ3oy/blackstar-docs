# Validate Pre-Approval OTP for Recurring Payment Plan

## Overview

The `Validate Pre-Approval OTP` endpoint allows you to verify an OTP (One-Time Password) to authorize the pre-approval of a recurring payment plan. This endpoint is specifically designed for recurring payment plans in the `PENDING_VERIFICATION_PREAPPROVAL` status. Upon successful validation, the OTP is confirmed, and the pre-approval process is authorized.

---

## Endpoint Details

### HTTP Method

**POST**

### URL

```
/api/rpp/client/{clientId}/portfolio/{portfolioId}/{rppId}/validate-preapproval-otp
```

---

## Parameters

| Name          | Description                 | Type   | Format | Required | Location |
| ------------- | --------------------------- | ------ | ------ | -------- | -------- |
| `clientId`    | Client UUID                 | string | $uuid  | Yes      | Path     |
| `portfolioId` | Portfolio UUID              | string | $uuid  | Yes      | Path     |
| `rppId`       | Recurring Payment Plan UUID | string | $uuid  | Yes      | Path     |

---

## Request Body

The request body must be in `application/json` format and includes the following fields:

| Field            | Type   | Description                                   |
| ---------------- | ------ | --------------------------------------------- |
| `customerMsisdn` | string | The customer's mobile number (MSISDN).        |
| `otpCode`        | string | The One-Time Password (OTP) sent to the user. |

#### Example Request Body

```json
{
  "customerMsisdn": "978946823235",
  "otpCode": "1396"
}
```

---

## Responses

### 200 OK

The OTP was successfully verified, and the pre-approval process was authorized.

#### Example Response Body

```json
true
```

---

### 400 Bad Request

The OTP or input data is invalid.

#### Example Response Body

```json
true
```

---

## Examples

### CURL Example

```bash
curl -X POST "https://api.example.com/api/rpp/client/{clientId}/portfolio/{portfolioId}/{rppId}/validate-preapproval-otp" \
-H "Content-Type: application/json" \
-H "Accept: */*" \
-d '{
  "customerMsisdn": "978946823235",
  "otpCode": "1396"
}'
```

#### Explanation:

- Replace `{clientId}`, `{portfolioId}`, and `{rppId}` with valid UUIDs.
- The `Content-Type` header is set to `application/json`.
- The `-d` flag specifies the JSON payload containing the customer's MSISDN and OTP code.

---

### JavaScript (Axios) Example

```javascript
const axios = require("axios");

const clientId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual client UUID
const portfolioId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual portfolio UUID
const rppId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual recurring payment plan UUID

const requestData = {
  customerMsisdn: "978946823235",
  otpCode: "1396",
};

axios
  .post(
    `https://api.example.com/api/rpp/client/${clientId}/portfolio/${portfolioId}/${rppId}/validate-preapproval-otp`,
    requestData,
    {
      headers: {
        "Content-Type": "application/json",
        Accept: "*/*",
      },
    }
  )
  .then((response) => {
    console.log("Response:", response.data);
  })
  .catch((error) => {
    console.error(
      "Error:",
      error.response ? error.response.data : error.message
    );
  });
```

#### Explanation:

- Replace `clientId`, `portfolioId`, and `rppId` with valid UUIDs.
- The `requestData` object contains the JSON payload for the request body.
- The `Content-Type` and `Accept` headers are set appropriately.

---

## Notes

1. Ensure that the `clientId`, `portfolioId`, and `rppId` are valid UUIDs.
2. The OTP must match the one sent to the user for verification.
3. If the OTP is invalid or expired, a `400 Bad Request` response will be returned.
4. The endpoint is only applicable for recurring payment plans in the `PENDING_VERIFICATION_PREAPPROVAL` status.
