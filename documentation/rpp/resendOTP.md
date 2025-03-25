# Resend OTP for Recurring Payment Plan Verification

## Overview

The `Resend OTP` endpoint allows you to trigger a new OTP (One-Time Password) for verifying a recurring payment plan. This is useful when the original OTP has expired or was not received by the user.

---

## Endpoint Details

### HTTP Method

**POST**

### URL

```
/api/rpp/client/{clientId}/portfolio/{portfolioId}/{rppId}/resend-otp
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

The request body must be in `application/json` format and includes the following field:

| Field         | Type   | Description                                                    |
| ------------- | ------ | -------------------------------------------------------------- |
| `referenceId` | string | The reference ID associated with the OTP verification process. |

#### Example Request Body

```json
{
  "referenceId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

---

## Responses

### 200 OK

The OTP was successfully resent.

#### Example Response Body

```
3fa85f64-5717-4562-b3fc-2c963f66afa6
```

---

### 400 Bad Request

The input data is invalid.

#### Example Response Body

```
3fa85f64-5717-4562-b3fc-2c963f66afa6
```

---

## Examples

### CURL Example

```bash
curl -X POST "https://api.example.com/api/rpp/client/{clientId}/portfolio/{portfolioId}/{rppId}/resend-otp" \
-H "Content-Type: application/json" \
-H "Accept: */*" \
-d '{
  "referenceId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}'
```

#### Explanation:

- Replace `{clientId}`, `{portfolioId}`, and `{rppId}` with valid UUIDs.
- The `Content-Type` header is set to `application/json`.
- The `-d` flag specifies the JSON payload containing the reference ID.

---

### JavaScript (Axios) Example

```javascript
const axios = require("axios");

const clientId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual client UUID
const portfolioId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual portfolio UUID
const rppId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual recurring payment plan UUID

const requestData = {
  referenceId: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
};

axios
  .post(
    `https://api.example.com/api/rpp/client/${clientId}/portfolio/${portfolioId}/${rppId}/resend-otp`,
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
2. The `referenceId` should correspond to the OTP verification process initiated earlier.
3. If the input data is invalid, a `400 Bad Request` response will be returned.
