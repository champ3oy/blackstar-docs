# Get Mobile Money Name

## Overview

The `Get Mobile Money Name` endpoint retrieves the name associated with a mobile money account based on the provided mobile number and mobile money provider. This endpoint requires one mandatory path parameter (`clientId`) and a JSON request body containing the mobile number and provider details.

---

## Endpoint Details

### HTTP Method

**POST**

### URL

```
/api/client/{clientId}/mobile-money/name
```

---

## Parameters

| Name       | Description | Type   | Format | Required | Location |
| ---------- | ----------- | ------ | ------ | -------- | -------- |
| `clientId` | Client UUID | string | $uuid  | Yes      | Path     |

---

## Request Body

The request body must be in `application/json` format and include the following fields:

| Field                 | Type   | Description                                                 |
| --------------------- | ------ | ----------------------------------------------------------- |
| `mobileNumber`        | string | The mobile number associated with the mobile money account. |
| `mobileMoneyProvider` | string | The provider of the mobile money service (e.g., `MTN_GH`).  |

#### Example Request Body

```json
{
  "mobileNumber": "233123456789",
  "mobileMoneyProvider": "MTN_GH"
}
```

---

## Responses

### 200 OK

The request was successful, and the mobile money name was retrieved.

#### Example Response Body

```json
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "mobileNumber": "233123456789",
  "mobileMoneyProvider": "MTN_GH",
  "verified": true,
  "mobileMoneyName": "John Doe",
  "verificationErrorMessage": "",
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
curl -X POST "https://api.example.com/api/client/{clientId}/mobile-money/name" \
-H "Content-Type: application/json" \
-H "Accept: */*" \
-d '{
  "mobileNumber": "233123456789",
  "mobileMoneyProvider": "MTN_GH"
}'
```

#### Explanation:

- Replace `{clientId}` with a valid UUID.
- The `Content-Type` header is set to `application/json`.
- The `-d` flag specifies the JSON request body containing the mobile number and provider.

---

### JavaScript (Axios) Example

```javascript
const axios = require("axios");

const clientId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual client UUID

const requestData = {
  mobileNumber: "233123456789",
  mobileMoneyProvider: "MTN_GH",
};

axios
  .post(
    `https://api.example.com/api/client/${clientId}/mobile-money/name`,
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

- Replace `clientId` with a valid UUID.
- The `requestData` object contains the JSON payload for the request body.
- The `Content-Type` and `Accept` headers are set appropriately.

---

## Notes

1. Ensure that the `clientId` is a valid UUID.
2. The `mobileNumber` should be in international format (e.g., `233123456789` for Ghana).
3. The `mobileMoneyProvider` should match the supported providers (e.g., `MTN_GH` for MTN Ghana).
4. If the `verified` field is `false`, check the `verificationErrorMessage` for details on why the verification failed.
5. The `otpReferenceId` can be used for further actions, such as OTP validation, if applicable.
