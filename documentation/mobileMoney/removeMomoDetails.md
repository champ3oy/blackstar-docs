# Remove Mobile Money Detail

## Overview

The `Remove Mobile Money Detail` endpoint is used to delete a specific mobile money account associated with a client. This endpoint requires two mandatory path parameters: `clientId` and `mobileMoneyID`. Upon successful deletion, it confirms that the mobile money detail has been removed.

---

## Endpoint Details

### HTTP Method

**DELETE**

### URL

```
/api/client/{clientId}/mobile-money/{mobileMoneyID}/delete
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

The request was successful, and the mobile money detail was removed.

#### Example Response Body

```json
{
  "message": "Mobile money detail removed successfully",
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "mobileNumber": "233123456789",
  "mobileMoneyProvider": "MTN_GH"
}
```

#### Response Fields

| Field                 | Type   | Description                                              |
| --------------------- | ------ | -------------------------------------------------------- |
| `message`             | string | Confirmation message indicating success.                 |
| `id`                  | string | Unique identifier for the mobile money account.          |
| `mobileNumber`        | string | The mobile number associated with the account.           |
| `mobileMoneyProvider` | string | The provider of the mobile money service (e.g., MTN_GH). |

---

## Examples

### CURL Example

```bash
curl -X DELETE "https://api.example.com/api/client/{clientId}/mobile-money/{mobileMoneyID}/delete" \
-H "Accept: */*"
```

#### Explanation:

- Replace `{clientId}` and `{mobileMoneyID}` with valid UUIDs.
- The `Accept` header is set to `*/*`.

---

### JavaScript (Axios) Example

```javascript
const axios = require("axios");

const clientId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual client UUID
const mobileMoneyID = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual mobile money UUID

axios
  .delete(
    `https://api.example.com/api/client/${clientId}/mobile-money/${mobileMoneyID}/delete`,
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

---

## Notes

1. Ensure that the `clientId` and `mobileMoneyID` are valid UUIDs.
2. Once a mobile money detail is deleted, it cannot be recovered. Use this endpoint with caution.
3. If the deletion fails, check the error message in the response for details on why the operation was unsuccessful.
