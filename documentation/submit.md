# Submit KYC

Submits a Know Your Customer (KYC) application for review.

## Endpoint Details

- **URL:** `/api/kyc/{kycId}/submit`
- **Method:** PUT
- **Description:** Submit KYC for review

## Parameters

| Name  | Located In | Description                               | Required | Schema        |
| ----- | ---------- | ----------------------------------------- | -------- | ------------- |
| kycId | path       | Unique identifier for the KYC application | Yes      | string (UUID) |

## Request

This endpoint doesn't require a request body.

## Response

### Success Response

- **Code:** 200 OK
- **Content-Type:** application/json

### Response Body Schema

```json
{
  "id": "string (UUID)",
  "userId": "string (UUID)",
  "updatedOn": "string (date-time)",
  "kycStatus": "string",
  "name": "string",
  "userKYCAnswerList": [
    {
      "id": "string (UUID)",
      "answer": "string",
      "questionIdentifier": "string",
      "question": "string",
      "sectionIdentifier": "string",
      "sectionName": "string",
      "subSectionIdentifier": "string",
      "subSectionName": "string",
      "questionType": "string",
      "multipleChoiceAnswer": ["string"]
    }
  ],
  "kycFormDTO": {
    "id": "string (UUID)",
    "name": "string",
    "description": "string",
    "version": "integer",
    "kycFormSections": [
      {
        "id": "string (UUID)",
        "name": "string",
        "description": "string",
        "visibilityOrder": "integer",
        "repeat": "boolean",
        "identifier": "string",
        "version": "integer",
        "maxRepetition": "integer",
        "kycFormSubSections": [
          {
            "id": "string (UUID)",
            "name": "string",
            "description": "string",
            "visibilityOrder": "integer",
            "identifier": "string",
            "version": "integer",
            "kycFormQuestions": [
              {
                "id": "string (UUID)",
                "question": "string",
                "questionType": "string",
                "description": "string",
                "visibilityOrder": "integer",
                "identifier": "string",
                "showInGrid": "boolean",
                "version": "integer",
                "required": "boolean",
                "kycValue": "string",
                "optionValues": [
                  {
                    "id": "string (UUID)",
                    "optionValue": "string",
                    "visibilityOrder": "integer",
                    "visible": "boolean",
                    "version": "integer"
                  }
                ]
              }
            ]
          }
        ]
      }
    ]
  },
  "errorMessage": "string",
  "email": "string",
  "phone": "string",
  "rejectionReason": "string",
  "currentSectionIdentifier": "string"
}
```

## Example Usage

### Python

```python
import requests
import uuid

# Replace with your API base URL
base_url = "https://api.example.com"

# Replace with an actual KYC ID
kyc_id = str(uuid.uuid4())

url = f"{base_url}/api/kyc/{kyc_id}/submit"

headers = {
    "Authorization": "Bearer YOUR_ACCESS_TOKEN"
}

response = requests.put(url, headers=headers)

if response.status_code == 200:
    kyc_data = response.json()
    print("KYC submitted successfully:")
    print(f"KYC ID: {kyc_data['id']}")
    print(f"Status: {kyc_data['kycStatus']}")
else:
    print(f"Error submitting KYC: {response.status_code}")
    print(response.text)
```

## Notes

- Ensure that you replace `YOUR_ACCESS_TOKEN` with a valid authentication token.
- The `kycId` in the URL should be a valid UUID of an existing KYC application.
- The response includes detailed information about the submitted KYC, including user answers, form structure, and current status.
- Handle potential errors by checking the response status code and the `errorMessage` field in the response body.

Would you like me to explain any specific part of this documentation or move on to the next endpoint?
