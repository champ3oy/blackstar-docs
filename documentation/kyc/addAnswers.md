# Add KYC Answers API Documentation

## Endpoint Overview

- **URL**: `/api/kyc/add`
- **Method**: POST
- **Description**: This endpoint allows you to add KYC (Know Your Customer) answers for a user.

## Request

### Headers

| Header       | Value            | Description                    |
| ------------ | ---------------- | ------------------------------ |
| Content-Type | application/json | The format of the request body |

### Request Body

| Parameter       | Type   | Required | Description                                       |
| --------------- | ------ | -------- | ------------------------------------------------- |
| email           | string | Yes      | The email address of the user                     |
| phone           | string | Yes      | The phone number of the user                      |
| clientSubTypeId | UUID   | Yes      | The unique identifier for the client subtype      |
| questionAnswer  | object | Yes      | An object containing the answers to KYC questions |

#### Example Request Body:

```json
{
  "email": "user@example.com",
  "phone": "+1234567890",
  "clientSubTypeId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "questionAnswer": {
    "questionIdentifier": "answer",
    "questionIdentifier": "answer",
    "questionIdentifier": "answer"
  }
}
```

## Response

### Success Response

- **Code**: 200 OK
- **Content-Type**: application/json

#### Response Body

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
  "updatedOn": "2024-06-28T13:27:44.668Z",
  "kycStatus": "VERIFIED",
  "name": "John Doe",
  "userKYCAnswerList": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "answer": "Example answer",
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
    //
  },
  "errorMessage": null,
  "email": "user@example.com",
  "phone": "+1234567890",
  "rejectionReason": null,
  "currentSectionIdentifier": "S1"
}
```

## Example Code

### cURL

```bash
curl -X POST "https://api.uatdev.blackstargroup.ai/api/kyc/add" \
     -H "Content-Type: application/json" \
     -d '{
  "email": "user@example.com",
  "phone": "+1234567890",
  "clientSubTypeId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "questionAnswer": {
    "questionIdentifier": "answer",
    "questionIdentifier": "answer",
    "questionIdentifier": "answer"
  }
}'
```

### JavaScript (Axios)

```javascript
const axios = require("axios");

const data = {
  email: "user@example.com",
  phone: "+1234567890",
  clientSubTypeId: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  questionAnswer: {
    questionIdentifier: "answer",
    questionIdentifier: "answer",
    questionIdentifier: "answer",
  },
};

axios
  .post("https://api.uatdev.blackstargroup.ai/api/kyc/add", data, {
    headers: {
      "Content-Type": "application/json",
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

1. Ensure all required fields are provided in the request body.
2. The `questionAnswer` object should contain key-value pairs where the key is the question identifier and the value is an object containing the answer.
3. The response includes detailed information about the KYC submission, including the form structure and the user's answers.
4. Handle potential errors by checking the `errorMessage` field in the response.
5. The `kycStatus` field indicates the current status of the KYC process for the user.
