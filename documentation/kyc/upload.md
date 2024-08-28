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
  "identifier1": "string (UUID)",
  "identifier2": "string (UUID)",
  "identifier3": "string (UUID)"
}
```

The response contains key-value pairs where the key is the filename or a property name, and the value is the document ID of the uploaded file.

## Example Usage

### cURL

```bash
curl --location 'http://localhost:9090/api/kyc/e335f9dd-aea6-4c80-807f-4c5708a1df6f/upload' \
--header 'Authorization: Bearer Token' \
--form 'files[0].identifier="7629a60fb47145aab44d84cc37f4023a"' \
--form 'files[0].file=@"/C:/Users/Downloads/Client performance.png"' \
--form 'files[1].identifier="cbced6cbac4643bd80b6b73efe0ba615"' \
--form 'files[1].file=@"/C:/Users/Downloads/Relationship Manager.png"'
```

### JavaScript (Axios)

```javascript
const axios = require("axios");
const FormData = require("form-data");
const fs = require("fs");

async function uploadKYCFiles() {
  const kycId = "123e4567-e89b-12d3-a456-426614174000";
  const url = `https://api.uatdev.blackstargroup.ai/api/kyc/${kycId}/upload`;

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
