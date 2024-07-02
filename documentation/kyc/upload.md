# Upload File for KYC

Uploads a file for a Know Your Customer (KYC) application.

## Endpoint Details

- **URL:** `/api/kyc/{kycId}/upload`
- **Method:** POST
- **Description:** Upload file for KYC

## Parameters

| Name  | Located In | Description                               | Required | Schema        |
| ----- | ---------- | ----------------------------------------- | -------- | ------------- |
| kycId | path       | Unique identifier for the KYC application | Yes      | string (UUID) |

## Request

### Content-Type

- multipart/form-data

### Request Body

| Name  | Type           | Description              | Required |
| ----- | -------------- | ------------------------ | -------- |
| files | array of files | The files to be uploaded | Yes      |

## Response

### Success Response

- **Code:** 200 OK
- **Content-Type:** application/json

### Response Body Schema

```json
{
  "additionalProp1": "string (UUID)",
  "additionalProp2": "string (UUID)",
  "additionalProp3": "string (UUID)"
}
```

The response contains key-value pairs where the key is the filename or a property name, and the value is the UUID of the uploaded file.

## Example Usage

### cURL

```bash
curl -X POST "https://api.uatdev.gnii.ai/api/kyc/123e4567-e89b-12d3-a456-426614174000/upload" \
     -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
     -H "Content-Type: multipart/form-data" \
     -F "files=@/path/to/document1.pdf" \
     -F "files=@/path/to/document2.jpg"
```

### JavaScript (Axios)

```javascript
const axios = require("axios");
const FormData = require("form-data");
const fs = require("fs");

async function uploadKYCFiles() {
  const kycId = "123e4567-e89b-12d3-a456-426614174000";
  const url = `https://api.uatdev.gnii.ai/api/kyc/${kycId}/upload`;

  const formData = new FormData();
  formData.append("files", fs.createReadStream("/path/to/document1.pdf"));
  formData.append("files", fs.createReadStream("/path/to/document2.jpg"));

  try {
    const response = await axios.post(url, formData, {
      headers: {
        Authorization: "Bearer YOUR_ACCESS_TOKEN",
        ...formData.getHeaders(),
      },
    });

    console.log("Files uploaded successfully:", response.data);
  } catch (error) {
    console.error(
      "Error uploading files:",
      error.response ? error.response.data : error.message
    );
  }
}

uploadKYCFiles();
```

## Notes

- Replace `YOUR_ACCESS_TOKEN` with a valid authentication token.
- The `kycId` in the URL should be a valid UUID of an existing KYC application.
- You can upload multiple files in a single request by adding multiple `files` fields in the form data.
- The response will contain UUIDs for each successfully uploaded file, which can be used to reference these files in future API calls.
- Handle potential errors by checking the response status code and any error messages in the response body.
