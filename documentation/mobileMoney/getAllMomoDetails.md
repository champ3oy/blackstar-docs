# Get All Mobile Money Detail

## Overview

The `Get All Mobile Money Detail` endpoint retrieves all mobile money accounts associated with a specific client. This endpoint requires one mandatory path parameter (`clientId`) and returns a list of mobile money details for that client.

---

## Endpoint Details

### HTTP Method

**GET**

### URL

```
/api/client/{clientId}/mobile-money/all
```

---

## Parameters

| Name       | Description | Type   | Format | Required | Location |
| ---------- | ----------- | ------ | ------ | -------- | -------- |
| `clientId` | Client UUID | string | $uuid  | Yes      | Path     |

---

## Responses

### 200 OK

The request was successful, and the mobile money details were retrieved.

#### Example Response Body

```json
[
  {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "mobileNumber": "233123456789",
    "mobileMoneyProvider": "MTN_GH",
    "verified": true,
    "mobileMoneyName": "John Doe",
    "verificationErrorMessage": "",
    "otpReferenceId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
  },
  {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa7",
    "mobileNumber": "233987654321",
    "mobileMoneyProvider": "VODAFONE_GH",
    "verified": false,
    "mobileMoneyName": "Jane Doe",
    "verificationErrorMessage": "Verification failed: Invalid mobile number.",
    "otpReferenceId": "3fa85f64-5717-4562-b3fc-2c963f66afa7"
  }
]
```

#### Response Fields

Each object in the response array contains the following fields:

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
curl -X GET "https://api.example.com/api/client/{clientId}/mobile-money/all" \
-H "Accept: */*"
```

#### Explanation:

- Replace `{clientId}` with a valid UUID.
- The `Accept` header is set to `*/*`.

---

### JavaScript (Axios) Example

```javascript
const axios = require("axios");

const clientId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual client UUID

axios
  .get(`https://api.example.com/api/client/${clientId}/mobile-money/all`, {
    headers: {
      Accept: "*/*",
    },
  })
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

- Replace `clientId` with a valid UUID.
- The `Accept` header is set to `*/*`.

---

## Notes

1. Ensure that the `clientId` is a valid UUID.
2. The response is an array of objects, each representing a mobile money account associated with the client.
3. If the `verified` field is `false`, check the `verificationErrorMessage` for details on why the verification failed.
4. The `otpReferenceId` can be used for further actions, such as OTP validation, if applicable.
