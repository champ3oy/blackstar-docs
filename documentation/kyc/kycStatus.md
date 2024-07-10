# Check UserKYC Status

## Endpoint Overview

- **URL**: `/api/kyc/{userKYCID}/status/check`
- **Method**: GET
- **Description**: This endpoint allows you to check the status of a user's KYC (Know Your Customer) submission.

## Request

### Path Parameters

| Parameter | Type | Required | Description                                         |
| --------- | ---- | -------- | --------------------------------------------------- |
| userKYCID | UUID | Yes      | The unique identifier for the user's KYC submission |

### Headers

No specific headers are required for this endpoint.

## Response

### Success Response

- **Code**: 200 OK
- **Content-Type**: application/json

### Response Body

| Field                    | Type     | Description                                          |
| ------------------------ | -------- | ---------------------------------------------------- |
| id                       | UUID     | Unique identifier for the KYC submission             |
| userId                   | UUID     | Unique identifier for the user                       |
| updatedOn                | datetime | Timestamp of the last update                         |
| kycStatus                | string   | Current status of the KYC process (e.g., "VERIFIED") |
| name                     | string   | Name of the user                                     |
| userKYCAnswerList        | array    | List of user's answers to KYC questions              |
| kycFormDTO               | object   | Details of the KYC form structure                    |
| errorMessage             | string   | Any error message (if applicable)                    |
| email                    | string   | User's email address                                 |
| phone                    | string   | User's phone number                                  |
| rejectionReason          | string   | Reason for rejection (if applicable)                 |
| currentSectionIdentifier | string   | Identifier of the current section in the KYC process |

#### Example Response:

```json
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "userId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "updatedOn": "2024-06-28T13:30:53.946Z",
  "kycStatus": "VERIFIED",
  "name": "John Doe",
  "userKYCAnswerList": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "answer": "Software Engineer",
      "questionIdentifier": "Q1",
      "question": "What is your occupation?",
      "sectionIdentifier": "S1",
      "sectionName": "Personal Information",
      "subSectionIdentifier": "SS1",
      "subSectionName": "Employment Details",
      "questionType": "TEXT",
      "multipleChoiceAnswer": []
    }
  ],
  "kycFormDTO": {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "name": "Standard KYC Form",
    "description": "KYC form for individual customers",
    "version": 1,
    "kycFormSections": [
      {
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "name": "Personal Information",
        "description": "Basic personal details",
        "visibilityOrder": 1,
        "repeat": false,
        "identifier": "S1",
        "version": 1,
        "maxRepetition": 1,
        "kycFormSubSections": [
          {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "name": "Employment Details",
            "description": "Information about current employment",
            "visibilityOrder": 1,
            "identifier": "SS1",
            "version": 1,
            "kycFormQuestions": [
              {
                "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
                "question": "What is your occupation?",
                "questionType": "TEXT",
                "description": "Please provide your current job title",
                "visibilityOrder": 1,
                "identifier": "Q1",
                "showInGrid": true,
                "version": 1,
                "required": true,
                "kycValue": "",
                "optionValues": []
              }
            ]
          }
        ]
      }
    ]
  },
  "errorMessage": null,
  "email": "john.doe@example.com",
  "phone": "+1234567890",
  "rejectionReason": null,
  "currentSectionIdentifier": "S1"
}
```

## Example Code

### cURL

```bash
curl -X GET "https://api.uatdev.blackstargroup.ai/api/kyc/3fa85f64-5717-4562-b3fc-2c963f66afa6/status/check"
```

### JavaScript (Axios)

```javascript
const axios = require("axios");

const userKYCID = "3fa85f64-5717-4562-b3fc-2c963f66afa6";

axios
  .get(`https://api.uatdev.blackstargroup.ai/api/kyc/${userKYCID}/status/check`)
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

## Notes

1. The `userKYCID` in the URL path is required and should be a valid UUID.
2. The response includes detailed information about the user's KYC submission, including the current status, user details, and the full KYC form structure.
3. The `kycStatus` field indicates the current status of the KYC process for the user (e.g., "VERIFIED", "PENDING", "REJECTED").
4. If there are any errors or issues with the KYC submission, check the `errorMessage` and `rejectionReason` fields in the response.
5. The `kycFormDTO` object contains the complete structure of the KYC form, including all sections, subsections, and questions.
6. The `userKYCAnswerList` provides the user's responses to the KYC questions.
7. The `currentSectionIdentifier` indicates which section of the KYC form the user is currently on or has last completed.
