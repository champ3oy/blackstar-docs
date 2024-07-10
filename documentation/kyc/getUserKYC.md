# Get UserKYC - Deprecated

This endpoint retrieves the KYC (Know Your Customer) information for the authenticated user.

## Endpoint Details

- **URL**: `/api/kyc/get`
- **Method**: GET
- **Description**: Retrieves the KYC information, including form structure and user answers, for the authenticated user.

## Parameters

This endpoint does not require any parameters.

## Response

### Success Response

- **Code**: 200 OK
- **Content-Type**: application/json

### Response Body Structure

The response body contains a JSON object with the following structure:

- `id` (string, UUID): Unique identifier for the user's KYC record
- `userId` (string, UUID): Unique identifier of the user
- `updatedOn` (string, date-time): Timestamp of the last update
- `kycStatus` (string): Current status of the KYC (e.g., "VERIFIED")
- `name` (string): Name of the user
- `userKYCAnswerList` (array): List of user's answers to KYC questions
  - `id` (string, UUID): Unique identifier for the answer
  - `answer` (string): User's answer to the question
  - `questionIdentifier` (string): Identifier of the question
  - `question` (string): The question text
  - `sectionIdentifier` (string): Identifier of the section containing the question
  - `sectionName` (string): Name of the section
  - `subSectionIdentifier` (string): Identifier of the subsection
  - `subSectionName` (string): Name of the subsection
  - `questionType` (string): Type of the question (e.g., "DATE")
  - `multipleChoiceAnswer` (array of strings): Selected options for multiple-choice questions
- `kycFormDTO` (object): Structure of the KYC form
  - (This object follows the same structure as the response in the "Get KYC Questions" API)
- `errorMessage` (string): Any error message related to the KYC process
- `email` (string): User's email address
- `phone` (string): User's phone number
- `rejectionReason` (string): Reason for KYC rejection, if applicable
- `currentSectionIdentifier` (string): Identifier of the current section in the KYC process

### Response Body

```json
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "userId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "updatedOn": "2024-07-02T15:53:34.191Z",
  "kycStatus": "VERIFIED",
  "name": "string",
  "userKYCAnswerList": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "answer": "string",
      "questionIdentifier": "string",
      "question": "string",
      "sectionIdentifier": "string",
      "sectionName": "string",
      "subSectionIdentifier": "string",
      "subSectionName": "string",
      "questionType": "DATE",
      "multipleChoiceAnswer": ["string"]
    }
  ],
  "kycFormDTO": {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "name": "string",
    "description": "string",
    "version": 0,
    "kycFormSections": [
      {
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "name": "string",
        "description": "string",
        "visibilityOrder": 0,
        "repeat": true,
        "identifier": "string",
        "version": 0,
        "maxRepetition": 0,
        "kycFormSubSections": [
          {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "name": "string",
            "description": "string",
            "visibilityOrder": 0,
            "identifier": "string",
            "version": 0,
            "kycFormQuestions": [
              {
                "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
                "question": "string",
                "questionType": "DATE",
                "description": "string",
                "visibilityOrder": 0,
                "identifier": "string",
                "showInGrid": true,
                "version": 0,
                "required": true,
                "kycValue": "string",
                "optionValues": [
                  {
                    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
                    "optionValue": "string",
                    "visibilityOrder": 0,
                    "visible": true,
                    "version": 0
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

### cURL

```bash
curl -X GET "https://api.uatdev.blackstargroup.ai/api/kyc/get" \
     -H "Accept: application/json" \
     -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

### JavaScript (Axios)

```javascript
const axios = require("axios");

const url = "https://api.uatdev.blackstargroup.ai/api/kyc/get";

axios
  .get(url, {
    headers: {
      Accept: "application/json",
      Authorization: "Bearer YOUR_ACCESS_TOKEN",
    },
  })
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

## Notes

1. Ensure that you replace `YOUR_ACCESS_TOKEN` with a valid authentication token for the user whose KYC information you're requesting.
2. This endpoint returns both the user's KYC answers and the full KYC form structure, allowing for a comprehensive view of the user's KYC status and the questions they've answered.
3. The `kycStatus` field indicates the current state of the user's KYC process (e.g., "VERIFIED").
4. The `userKYCAnswerList` contains the user's responses to individual KYC questions, including details about the question's location within the form structure.
5. The `kycFormDTO` object provides the complete structure of the KYC form, which can be used to render the form or validate the user's answers.
6. If there are any issues with the user's KYC, the `errorMessage` and `rejectionReason` fields may contain relevant information.
7. The `currentSectionIdentifier` can be used to determine which part of the KYC process the user is currently on, which may be useful for multi-step KYC processes.
8. This endpoint does not require any parameters as it retrieves information for the authenticated user based on their access token.
