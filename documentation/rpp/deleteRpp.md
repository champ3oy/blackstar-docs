# Delete Recurring Payment Plan

## Overview

The `Delete Recurring Payment Plan` endpoint allows you to delete an existing recurring payment plan by its ID. This endpoint requires three mandatory path parameters: `clientId`, `portfolioId`, and `id`. Upon successful deletion, it confirms that the recurring payment plan has been removed.

---

## Endpoint Details

### HTTP Method

**DELETE**

### URL

```
/api/rpp/client/{clientId}/portfolio/{portfolioId}/{id}
```

---

## Parameters

| Name          | Description                 | Type   | Format | Required | Location |
| ------------- | --------------------------- | ------ | ------ | -------- | -------- |
| `clientId`    | Client UUID                 | string | $uuid  | Yes      | Path     |
| `portfolioId` | Portfolio UUID              | string | $uuid  | Yes      | Path     |
| `id`          | Recurring Payment Plan UUID | string | $uuid  | Yes      | Path     |

---

## Responses

### 200 OK

The request was successful, and the recurring payment plan was deleted.

#### Example Response Body

```json
{
  "message": "Recurring payment plan deleted successfully",
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

#### Response Fields

| Field     | Type   | Description                                               |
| --------- | ------ | --------------------------------------------------------- |
| `message` | string | Confirmation message indicating success.                  |
| `id`      | string | Unique identifier for the deleted recurring payment plan. |

---

### 404 Not Found

The recurring payment plan with the specified ID was not found.

#### Example Response Body

```json
{
  "error": "Recurring payment plan not found",
  "details": "No recurring payment plan exists with the provided ID."
}
```

---

## Examples

### CURL Example

```bash
curl -X DELETE "https://api.example.com/api/rpp/client/{clientId}/portfolio/{portfolioId}/{id}" \
-H "Accept: */*"
```

#### Explanation:

- Replace `{clientId}`, `{portfolioId}`, and `{id}` with valid UUIDs.
- The `Accept` header is set to `*/*`.

---

### JavaScript (Axios) Example

```javascript
const axios = require("axios");

const clientId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual client UUID
const portfolioId = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual portfolio UUID
const id = "3fa85f64-5717-4562-b3fc-2c963f66afa6"; // Replace with actual recurring payment plan UUID

axios
  .delete(
    `https://api.example.com/api/rpp/client/${clientId}/portfolio/${portfolioId}/${id}`,
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

- Replace `clientId`, `portfolioId`, and `id` with valid UUIDs.
- The `Accept` header is set to `*/*`.

---

## Notes

1. Ensure that the `clientId`, `portfolioId`, and `id` are valid UUIDs.
2. Once a recurring payment plan is deleted, it cannot be recovered. Use this endpoint with caution.
3. If the deletion fails, check the error message in the response for details on why the operation was unsuccessful.
