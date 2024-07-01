# Get KYC Questions

This endpoint retrieves KYC (Know Your Customer) questions based on the client subtype.

## Endpoint Details

- **URL**: `/api/kyc/{clientSubTypeId}/get-kyc`
- **Method**: GET
- **Description**: Retrieves a set of KYC questions and form structure for a specific client subtype.

## Parameters

| Name            | Type          | Location | Required | Description                                  |
| --------------- | ------------- | -------- | -------- | -------------------------------------------- |
| clientSubTypeId | string (UUID) | path     | Yes      | The unique identifier for the client subtype |

## Response

### Success Response

- **Code**: 200 OK
- **Content-Type**: application/json

### Response Body Structure

The response body contains a JSON object with the following structure:

- `id` (string, UUID): Unique identifier for the KYC form
- `name` (string): Name of the KYC form
- `description` (string): Description of the KYC form
- `version` (integer): Version number of the KYC form
- `kycFormSections` (array): List of form sections
  - `id` (string, UUID): Unique identifier for the section
  - `name` (string): Name of the section
  - `description` (string): Description of the section
  - `visibilityOrder` (integer): Order in which the section should be displayed
  - `repeat` (boolean): Whether the section can be repeated
  - `identifier` (string): Unique identifier string for the section
  - `version` (integer): Version number of the section
  - `maxRepetition` (integer): Maximum number of times the section can be repeated
  - `kycFormSubSections` (array): List of subsections within the section
    - `id` (string, UUID): Unique identifier for the subsection
    - `name` (string): Name of the subsection
    - `description` (string): Description of the subsection
    - `visibilityOrder` (integer): Order in which the subsection should be displayed
    - `identifier` (string): Unique identifier string for the subsection
    - `version` (integer): Version number of the subsection
    - `kycFormQuestions` (array): List of questions within the subsection
      - `id` (string, UUID): Unique identifier for the question
      - `question` (string): The actual question text
      - `questionType` (string): Type of the question (e.g., "DATE")
      - `description` (string): Description or additional information for the question
      - `visibilityOrder` (integer): Order in which the question should be displayed
      - `identifier` (string): Unique identifier string for the question
      - `showInGrid` (boolean): Whether the question should be shown in a grid view
      - `version` (integer): Version number of the question
      - `required` (boolean): Whether the question is mandatory
      - `kycValue` (string): Default or pre-filled value for the question
      - `optionValues` (array): List of options for multiple-choice questions
        - `id` (string, UUID): Unique identifier for the option
        - `optionValue` (string): The text of the option
        - `visibilityOrder` (integer): Order in which the option should be displayed
        - `visible` (boolean): Whether the option is visible
        - `version` (integer): Version number of the option

## Example Usage

### cURL

```bash
curl -X GET "https://api.example.com/api/kyc/3fa85f64-5717-4562-b3fc-2c963f66afa6/get-kyc" \
     -H "Accept: application/json" \
     -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

### JavaScript (Axios)

```javascript
const axios = require("axios");

const clientSubTypeId = "3fa85f64-5717-4562-b3fc-2c963f66afa6";
const url = `https://api.example.com/api/kyc/${clientSubTypeId}/get-kyc`;

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

1. Ensure that you replace `YOUR_ACCESS_TOKEN` with a valid authentication token.
2. The `clientSubTypeId` in the URL should be a valid UUID corresponding to an existing client subtype.
3. The response structure is hierarchical, allowing for a flexible form structure with sections, subsections, and questions.
4. The `questionType` field in the `kycFormQuestions` array indicates the type of input expected for each question. In the example, "DATE" is shown, but there may be other types available.
5. The `optionValues` array within each question object is used for questions that have predefined answer choices, such as multiple-choice questions.
6. The `version` fields throughout the response allow for tracking changes to different components of the KYC form over time.
7. The `visibilityOrder` fields can be used to determine the display order of sections, subsections, questions, and options in the user interface.

This API endpoint provides a comprehensive structure for KYC forms, allowing for dynamic form generation based on the client subtype. It supports complex form structures with repeatable sections and various question types.
