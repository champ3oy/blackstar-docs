# Validate Mobile Money Detail with OTP

## Overview

The `Validate Mobile Money Detail with OTP` endpoint is used to validate a mobile money account using an OTP (One-Time Password). This endpoint requires two mandatory path parameters (`clientId` and `mobileMoneyID`) and a JSON request body containing the OTP and reference ID. Upon successful validation, it returns a confirmation response.

---

## Endpoint Details

### HTTP Method

**POST**

### URL

```
/api/client/{clientId}/mobile-money/{mobileMoneyID}/validate
```

---

## Parameters

| Name            | Description       | Type   | Format | Required | Location |
| --------------- | ----------------- | ------ | ------ | -------- | -------- |
| `clientId`      | Client UUID       | string | $uuid  | Yes      | Path     |
| `mobileMoneyID` | Mobile Money UUID | string | $uuid  | Yes      | Path     |

---

## Request Body

The request body must be in `application/json` format and include the following fields:

| Field         | Type           | Description                                                                           |
| ------------- | -------------- | ------------------------------------------------------------------------------------- |
| `otp`         | string         | The One-Time Password (OTP) received by the user for validation.                      |
| `referenceID` | string ($uuid) | Reference ID associated with the OTP validation request (e.g., from a previous step). |

#### Example Request Body

```json
{
  "otp": "123456",
  "referenceID": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

---

## Responses

### 200 OK

The request was successful, and the OTP validation was completed.

#### Example Response Body

```json
{
  "message": "OTP validation successful"
}
```

---

## Examples

### CURL Example

```bash
curl -X POST "https://api.example.com/api/client/{clientId}/mobile-money/{mobileMoneyID}/validate" \
-H "Content-Type: application/json" \
-H "Accept: */*" \
-d '{
  "otp": "123456",
  "referenceID": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}'
```

#### Explanation:

- Replace `{clientId}` and `{mobileMoneyID}` with valid UUIDs.
- The `Content-Type` header is set to `application/json`.
- The `-d` flag specifies the JSON request body containing the OTP and reference ID.

---

### JavaScript (Axios) Example

```javascript
const axios = require("axios");

const clientId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual client UUID
const mobileMoneyID = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual mobile money UUID

const requestData = {
  otp: "123456",
  referenceID: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
};

axios
  .post(
    `https://api.example.com/api/client/${clientId}/mobile-money/${mobileMoneyID}/validate`,
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

- Replace `clientId` and `mobileMoneyID` with valid UUIDs.
- The `requestData` object contains the JSON payload for the request body.
- The `Content-Type` and `Accept` headers are set appropriately.

---

## Notes

1. Ensure that the `clientId` and `mobileMoneyID` are valid UUIDs.
2. The `otp` field must contain the exact OTP received by the user. It is case-sensitive and typically numeric.
3. The `referenceID` should match the reference ID provided during the initial verification step (e.g., from the `Verify Mobile Money Detail` endpoint).
