# Resend OTP for Mobile Money Verification

## Overview

The `Resend OTP for Mobile Money Verification` endpoint is used to resend a One-Time Password (OTP) for mobile money account verification. This endpoint requires two mandatory path parameters (`clientId` and `mobileMoneyID`) and a JSON request body containing the reference ID associated with the original OTP request. Upon successful execution, it confirms that the OTP has been resent.

---

## Endpoint Details

### HTTP Method

**POST**

### URL

```
/api/client/{clientId}/mobile-money/{mobileMoneyID}/resend
```

---

## Parameters

| Name            | Description       | Type   | Format | Required | Location |
| --------------- | ----------------- | ------ | ------ | -------- | -------- |
| `clientId`      | Client UUID       | string | $uuid  | Yes      | Path     |
| `mobileMoneyID` | Mobile Money UUID | string | $uuid  | Yes      | Path     |

---

## Request Body

The request body must be in `application/json` format and include the following field:

| Field         | Type           | Description                                                                                                   |
| ------------- | -------------- | ------------------------------------------------------------------------------------------------------------- |
| `referenceId` | string ($uuid) | Reference ID associated with the original OTP request (e.g., from the `Verify Mobile Money Detail` endpoint). |

#### Example Request Body

```json
{
  "referenceId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

---

## Responses

### 200 OK

The request was successful, and the OTP was resent.

#### Example Response Body

```json
{
  "message": "OTP resent successfully",
  "additionalProp1": "value1",
  "additionalProp2": "value2",
  "additionalProp3": "value3"
}
```

#### Response Fields

| Field             | Type   | Description                                     |
| ----------------- | ------ | ----------------------------------------------- |
| `message`         | string | Confirmation message indicating success.        |
| `additionalProp1` | string | Placeholder for additional properties (if any). |
| `additionalProp2` | string | Placeholder for additional properties (if any). |
| `additionalProp3` | string | Placeholder for additional properties (if any). |

---

## Examples

### CURL Example

```bash
curl -X POST "https://api.example.com/api/client/{clientId}/mobile-money/{mobileMoneyID}/resend" \
-H "Content-Type: application/json" \
-H "Accept: */*" \
-d '{
  "referenceId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}'
```

#### Explanation:

- Replace `{clientId}` and `{mobileMoneyID}` with valid UUIDs.
- The `Content-Type` header is set to `application/json`.
- The `-d` flag specifies the JSON request body containing the `referenceId`.

---

### JavaScript (Axios) Example

```javascript
const axios = require("axios");

const clientId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual client UUID
const mobileMoneyID = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual mobile money UUID

const requestData = {
  referenceId: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
};

axios
  .post(
    `https://api.example.com/api/client/${clientId}/mobile-money/${mobileMoneyID}/resend`,
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
2. The `referenceId` should match the reference ID provided during the initial verification step (e.g., from the `Verify Mobile Money Detail` endpoint).
3. If additional properties (`additionalProp1`, `additionalProp2`, etc.) are returned in the response, they may contain supplementary information about the OTP resend process.
