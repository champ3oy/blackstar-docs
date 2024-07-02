# Get KYC Answers API Documentation

## Endpoint Overview

- **URL**: `/api/kyc/{kycId}/{subSectionIdentifier}/answer/get`
- **Method**: GET
- **Description**: This endpoint retrieves KYC (Know Your Customer) answers for a specific subsection of a user's KYC submission.

## Request

### Path Parameters

| Parameter            | Type   | Required | Description                                   |
| -------------------- | ------ | -------- | --------------------------------------------- |
| kycId                | UUID   | Yes      | The unique identifier for the KYC submission  |
| subSectionIdentifier | string | Yes      | The identifier of the specific KYC subsection |

### Headers

No specific headers are required for this endpoint.

## Response

### Success Response

- **Code**: 200 OK
- **Content-Type**: application/json

### Response Body

The response is an array of objects, each representing an answer to a KYC question within the specified subsection.

| Field                | Type   | Description                                            |
| -------------------- | ------ | ------------------------------------------------------ |
| id                   | UUID   | Unique identifier for this specific answer             |
| answer               | string | The user's answer to the question                      |
| questionIdentifier   | string | Unique identifier for the question                     |
| question             | string | The text of the question                               |
| sectionIdentifier    | string | Identifier for the section containing this question    |
| sectionName          | string | Name of the section                                    |
| subSectionIdentifier | string | Identifier for the subsection containing this question |
| subSectionName       | string | Name of the subsection                                 |
| questionType         | string | Type of the question (e.g., "DATE", "TEXT", "CHOICE")  |
| multipleChoiceAnswer | array  | List of selected answers for multiple-choice questions |

#### Example Response:

```json
[
  {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "answer": "1234567890001",
    "questionIdentifier": "b619569d86884806860d39c7598ca4a1",
    "question": "Account Number",
    "sectionIdentifier": "S1",
    "sectionName": "Personal Information",
    "subSectionIdentifier": "e619569d86884806860d39c7598ca4a1",
    "subSectionName": "Account Information",
    "questionType": "NUMERIC",
    "multipleChoiceAnswer": []
  },
  {
    "id": "4fa85f64-5717-4562-b3fc-2c963f66afa7",
    "answer": "2022-03-15",
    "questionIdentifier": "Q2",
    "question": "Date of Birth",
    "sectionIdentifier": "a619569d86884806860d39c7598ca4a1",
    "sectionName": "Personal Information",
    "subSectionIdentifier": "c619569d86884806860d39c7598ca4a1",
    "subSectionName": "User Information",
    "questionType": "DATE",
    "multipleChoiceAnswer": []
  },
  ...
]
```

## Example Code

### cURL

```bash
curl -X GET "https://api.example.com/api/kyc/3fa85f64-5717-4562-b3fc-2c963f66afa6/SS1/answer/get"
```

### JavaScript (Axios)

```javascript
const axios = require("axios");

const kycId = "3fa85f64-5717-4562-b3fc-2c963f66afa6";
const subSectionIdentifier = "SS1";

axios
  .get(
    `https://api.example.com/api/kyc/${kycId}/${subSectionIdentifier}/answer/get`
  )
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

## Notes

1. The `kycId` in the URL path should be a valid UUID corresponding to a specific KYC submission.
2. The `subSectionIdentifier` should match a valid subsection within the KYC form structure.
3. This endpoint returns answers only for the specified subsection. To get answers for other subsections, you'll need to make separate API calls with different `subSectionIdentifier` values.
4. The `questionType` field indicates the type of question, which can help in properly interpreting and displaying the answer.
5. For multiple-choice questions, check the `multipleChoiceAnswer` array for selected options.
6. If no answers are found for the given KYC ID and subsection, the API will return an empty array.
7. Ensure proper error handling in your code to deal with potential API errors or empty responses.
