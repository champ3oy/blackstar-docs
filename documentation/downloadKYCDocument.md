# Download KYC Document API Documentation

## Endpoint Overview

- **URL**: `/api/kyc/{kycId}/document/{docId}/download`
- **Method**: GET
- **Description**: This endpoint allows you to download a specific document that was uploaded as part of a KYC (Know Your Customer) submission.

## Request

### Path Parameters

| Parameter | Type | Required | Description                                     |
| --------- | ---- | -------- | ----------------------------------------------- |
| kycId     | UUID | Yes      | The unique identifier for the KYC submission    |
| docId     | UUID | Yes      | The unique identifier for the specific document |

### Headers

No specific headers are required for this endpoint.

## Response

### Success Response

- **Code**: 200 OK
- **Content-Type**: Depends on the type of document (e.g., application/pdf, image/jpeg, etc.)

### Response Body

The response body will contain the binary data of the requested document.

## Example Code

### cURL

```bash
curl -X GET "https://api.example.com/api/kyc/3fa85f64-5717-4562-b3fc-2c963f66afa6/document/4fa85f64-5717-4562-b3fc-2c963f66afa7/download" --output document.pdf
```

### JavaScript (Axios)

```javascript
const axios = require("axios");
const fs = require("fs");

const kycId = "3fa85f64-5717-4562-b3fc-2c963f66afa6";
const docId = "4fa85f64-5717-4562-b3fc-2c963f66afa7";

axios({
  method: "get",
  url: `https://api.example.com/api/kyc/${kycId}/document/${docId}/download`,
  responseType: "stream",
})
  .then((response) => {
    response.data.pipe(fs.createWriteStream("document.pdf"));
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

## Notes

1. The `kycId` in the URL path should be a valid UUID corresponding to a specific KYC submission.
2. The `docId` should be a valid UUID corresponding to a specific document within the KYC submission.
3. The response will be the binary data of the document, not a JSON object.
4. The Content-Type of the response will vary depending on the type of document being downloaded (e.g., PDF, JPEG, PNG).
5. When implementing this in a frontend application, you may need to handle the binary data appropriately, typically by creating a Blob and a download link.
6. Ensure that you have the necessary permissions to access the document before making the request.
7. Large documents may take longer to download. Consider implementing a loading indicator in your application.
8. If the document is not found or there's an error, the API may return an appropriate error status code instead of 200.

### Error Handling

Possible error responses:

- 404 Not Found: If the KYC submission or the document doesn't exist.
- 403 Forbidden: If the user doesn't have permission to access the document.
- 500 Internal Server Error: For any server-side issues.

Ensure your application handles these potential error scenarios gracefully.

### Security Considerations

1. Ensure that only authorized users can access this endpoint.
2. Validate the `kycId` and `docId` on the server-side to prevent unauthorized access to documents.
3. Consider implementing rate limiting to prevent abuse of the API.

Remember to replace `https://api.example.com` with the actual base URL of your API when making requests.
