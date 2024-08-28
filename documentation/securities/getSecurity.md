# Get Fund Particular

This API endpoint retrieves specific details about a security/product associated with a given security ID.

## Endpoint

```
GET /api/product/{securityID}/fundParticular
```

## Description

Retrieves the particulars of a fund based on the provided security ID.

## Parameters

| Name       | Type   | In   | Description                                                                   |
| ---------- | ------ | ---- | ----------------------------------------------------------------------------- |
| securityID | string | path | The unique identifier for security (UUID format). This parameter is required. |

## Response

### Successful Response (200 OK)

The response will be a JSON object containing the particulars of the fund. The structure of the response may include additional properties.

#### Example Response

```json
{
   "data" : base 64 encoded bytes,
   "meta" : { "filename" : name of file}
}
```

### Response Codes

- `200 OK`: Request was successful and the response body contains the fund particulars.
- Other codes may indicate errors (e.g., `400 Bad Request`, `404 Not Found`).

## Example Request and Response

### Example Request

```bash
curl -X GET "https://api.example.com/api/product/{securityID}/fundParticular" -H "accept: */*"
```

```javascript
const axios = require("axios");

axios
  .get("https://api.example.com/api/product/{securityID}/fundParticular")
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error(error);
  });
```

### Example Response

```json
{
   "data" : base 64 encoded bytes,
   "meta" : { "filename" : name of file}
}
```

## Notes

- Ensure the `securityID` provided is in the correct UUID format.
- Check for response codes to handle different scenarios (e.g., error handling for `404 Not Found` if the security ID does not exist).
