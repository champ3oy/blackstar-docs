# Upload File for KYC Using Link

Uploads a file for a Know Your Customer (KYC) application using a publicly accessible file link.

## Endpoint Details

- **URL:** `/api/kyc/{kycId}/upload/link`
- **Method:** POST
- **Description:** Upload file for KYC using a file link

## Parameters

| Name  | Located In | Description                               | Required | Schema        |
| ----- | ---------- | ----------------------------------------- | -------- | ------------- |
| kycId | path       | Unique identifier for the KYC application | Yes      | string (UUID) |

## Request

### Content-Type

- application/json

### Request Body

| Name       | Type   | Description                                     | Required |
| ---------- | ------ | ----------------------------------------------- | -------- |
| files      | array  | Array of file objects                           | Yes      |
| identifier | string | Unique identifier corresponding to the question | Yes      |
| imageLink  | string | Publicly accessible URL of the file             | Yes      |

### Request Body Schema

```json
{
  "files": [
    {
      "identifier": "string (UUID)",
      "imageLink": "string (URL)"
    }
  ]
}
```

## Response

### Success Response

- **Code:** 200 OK
- **Content-Type:** application/json

### Response Body Schema

```json
{
  "file-name1": "question-identifier1",
  "file-name2": "question-identifier2"
}
```

The response contains key-value pairs where the key is the filename and the value is the question identifier associated with the uploaded file.

## Example Usage

### cURL

```bash
curl --location 'http://localhost:9090/api/kyc/e335f9dd-aea6-4c80-807f-4c5708a1df6f/upload/link' \
--header 'Authorization: Bearer Token' \
--header 'Content-Type: application/json' \
--data '{
    "files": [
        {
            "identifier": "c30a83ca88b2499cb30c592657e91122",
            "imageLink": "https://example.com/path/to/file1.pdf"
        },
        {
            "identifier": "d40b94db99c3500dc41d603768f02233",
            "imageLink": "https://example.com/path/to/file2.jpg"
        }
    ]
}'
```

### JavaScript (Axios)

```javascript
const axios = require("axios");

async function uploadKYCFilesWithLink() {
  const kycId = "123e4567-e89b-12d3-a456-426614174000";
  const url = `https://api.uatdev.blackstargroup.ai/api/kyc/${kycId}/upload/link`;

  const requestBody = {
    files: [
      {
        identifier: "c30a83ca88b2499cb30c592657e91122",
        imageLink: "https://example.com/path/to/file1.pdf",
      },
      {
        identifier: "d40b94db99c3500dc41d603768f02233",
        imageLink: "https://example.com/path/to/file2.jpg",
      },
    ],
  };

  try {
    const response = await axios.post(url, requestBody, {
      headers: {
        Authorization: "Bearer YOUR_ACCESS_TOKEN",
        "Content-Type": "application/json",
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

uploadKYCFilesWithLink();
```

## Notes

- Replace `YOUR_ACCESS_TOKEN` with a valid authentication token.
- The `kycId` in the URL should be a valid UUID of an existing KYC application.
- You can upload multiple files in a single request by adding multiple file objects in the request body.
- Maximum file size allowed is 5 MB.
- The response will contain mappings between file names and their associated question identifiers.
- All file links must be publicly accessible.
- Handle potential errors by checking the response status code and any error messages in the response body.
