# Verify Mobile Money Detail

## Overview

The `Verify Mobile Money Detail` endpoint is used to verify the details of a mobile money account associated with a specific client. This endpoint requires two mandatory path parameters: `clientId` and `mobileMoneyID`. Upon successful verification, it returns detailed information about the mobile money account.

---

## Endpoint Details

### HTTP Method

**PUT**

### URL

```
/put_api_client/{clientId}/mobile-money/{mobileMoneyID}/verify
```

---

## Parameters

| Name            | Description       | Type   | Format | Required | Location |
| --------------- | ----------------- | ------ | ------ | -------- | -------- |
| `clientId`      | Client UUID       | string | $uuid  | Yes      | Path     |
| `mobileMoneyID` | Mobile Money UUID | string | $uuid  | Yes      | Path     |

---

## Responses

### 200 OK

The request was successful, and the mobile money details were verified.

#### Example Response Body

```json
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "mobileNumber": "string",
  "mobileMoneyProvider": "MTN_GH",
  "verified": true,
  "mobileMoneyName": "string",
  "verificationErrorMessage": "string",
  "otpReferenceId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

#### Response Fields

| Field                      | Type    | Description                                              |
| -------------------------- | ------- | -------------------------------------------------------- |
| `id`                       | string  | Unique identifier for the mobile money account.          |
| `mobileNumber`             | string  | The mobile number associated with the account.           |
| `mobileMoneyProvider`      | string  | The provider of the mobile money service (e.g., MTN_GH). |
| `verified`                 | boolean | Indicates whether the account was successfully verified. |
| `mobileMoneyName`          | string  | The name associated with the mobile money account.       |
| `verificationErrorMessage` | string  | Error message if verification fails.                     |
| `otpReferenceId`           | string  | Reference ID for OTP verification (if applicable).       |

---

## Examples

### CURL Example

```bash
curl -X PUT "https://api.example.com/put_api_client/{clientId}/mobile-money/{mobileMoneyID}/verify" \
-H "Accept: */*"
```

#### Explanation:

- Replace `{clientId}` and `{mobileMoneyID}` with valid UUIDs.
- The `Accept` header is set to `*/*` to accept any media type.

---

### JavaScript (Axios) Example

```javascript
const axios = require("axios");

const clientId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual client UUID
const mobileMoneyID = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual mobile money UUID

axios
  .put(
    `https://api.example.com/put_api_client/${clientId}/mobile-money/${mobileMoneyID}/verify`,
    null,
    {
      headers: {
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
- The `Accept` header is set to `*/*`.
- The `null` in the `axios.put` method indicates that no request body is required for this endpoint.

---

## Notes

1. Ensure that the `clientId` and `mobileMoneyID` are valid UUIDs.
2. If the verification fails, check the `verificationErrorMessage` field in the response for details.
3. The `otpReferenceId` can be used for further actions, such as OTP validation, if applicable.
