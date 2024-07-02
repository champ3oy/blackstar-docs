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
       
### Response Body
```json
{
    "id": "07c817de-c3ad-4e61-a020-ea4d623fc3cb",
    "name": "individual",
    "description": null,
    "version": 82,
    "kycFormSections": [
        {
            "id": "f932aeb9-e60f-4a6e-a09e-04238f6b919e",
            "name": "Black Star Individual KYC Form",
            "description": null,
            "visibilityOrder": null,
            "repeat": false,
            "identifier": "4142d878aa3d4167a2ec8c0c717e3dc2",
            "version": 69,
            "maxRepetition": null,
            "kycFormSubSections": [
                {
                    "id": "a72f7acc-5c92-4d66-b7bc-05a47dc020e2",
                    "name": "Personal & address information",
                    "description": null,
                    "visibilityOrder": 0,
                    "identifier": "23cf54e2b437409886bd55530d6755ae",
                    "version": 19,
                    "kycFormQuestions": [
                        {
                            "id": "80752ba7-ed30-46ce-8fae-5cf10a55ecc0",
                            "question": "Phone number",
                            "questionType": "PHONE_NUMBER",
                            "description": "209335976",
                            "visibilityOrder": 0,
                            "identifier": "0c9d672c8d024418aafb0bc0dea1225b",
                            "showInGrid": false,
                            "version": 7,
                            "required": true,
                            "kycValue": null,
                            "optionValues": []
                        },
                        {
                            "id": "f1022538-238f-41bb-9a1d-1545212e44fc",
                            "question": "Region",
                            "questionType": "SINGLE_LINE",
                            "description": null,
                            "visibilityOrder": 3,
                            "identifier": "17f822e94c994475891acad4a26f92b9",
                            "showInGrid": false,
                            "version": 2,
                            "required": false,
                            "kycValue": null,
                            "optionValues": []
                        },
                        {
                            "id": "3ab1a16f-91b7-4ed8-88a1-ffaeeda71552",
                            "question": "Country",
                            "questionType": "SINGLE_CHOICE",
                            "description": null,
                            "visibilityOrder": 4,
                            "identifier": "487c0384203246f2874e52d4148ef5d9",
                            "showInGrid": false,
                            "version": 2,
                            "required": true,
                            "kycValue": null,
                            "optionValues": [
                                {
                                    "id": "23242657-99ff-440e-b146-44c9ef27cbad",
                                    "optionValue": "India",
                                    "visibilityOrder": null,
                                    "visible": false,
                                    "version": null
                                },
                                {
                                    "id": "df146eeb-5230-483e-8a7d-44979fb68351",
                                    "optionValue": "USA",
                                    "visibilityOrder": null,
                                    "visible": false,
                                    "version": null
                                }
                            ]
                        },
                    ]
                },
                {
                    "id": "aa908a5f-0c77-4569-b86a-53f654f13ade",
                    "name": "Emergency Contact information",
                    "description": null,
                    "visibilityOrder": 1,
                    "identifier": "97ce6017f76c41189029028783e4dc91",
                    "version": 11,
                    "kycFormQuestions": [
                        {
                            "id": "8ba88a3e-f876-4508-b2dc-4b8f8992188e",
                            "question": "Date of birth",
                            "questionType": "DATE",
                            "description": null,
                            "visibilityOrder": 0,
                            "identifier": "0591b4749c2d43b39626e51ef6109124",
                            "showInGrid": false,
                            "version": 2,
                            "required": false,
                            "kycValue": null,
                            "optionValues": []
                        },
                        {
                            "id": "91ba1307-e5b8-4cb7-9ff9-3a0fb5fba191",
                            "question": "Contact Number",
                            "questionType": "PHONE_NUMBER",
                            "description": null,
                            "visibilityOrder": 1,
                            "identifier": "4bfdc1c7fb6c40d9a59009d8598647ff",
                            "showInGrid": false,
                            "version": 2,
                            "required": false,
                            "kycValue": null,
                            "optionValues": []
                        },
                    ]
                },
                {
                    "id": "8070412e-dab4-48ba-b28c-474a352c3a33",
                    "name": "Professional & financial information",
                    "description": null,
                    "visibilityOrder": 2,
                    "identifier": "69e18fc24b2b4ffeb00a776d7eb3df36",
                    "version": 15,
                    "kycFormQuestions": [
                        {
                            "id": "2ed4ce43-055c-42b4-83fc-5772017824e6",
                            "question": "Employment status",
                            "questionType": "SINGLE_CHOICE",
                            "description": null,
                            "visibilityOrder": 0,
                            "identifier": "26000159d5774235b5cf8535850ee154",
                            "showInGrid": false,
                            "version": 2,
                            "required": true,
                            "kycValue": null,
                            "optionValues": [
                                {
                                    "id": "f8d6bb28-7cdf-41d1-a982-6f36be12bdba",
                                    "optionValue": "Employed",
                                    "visibilityOrder": null,
                                    "visible": false,
                                    "version": null
                                },
                                {
                                    "id": "fae5b2cd-99ce-4a5f-9069-6d5820f292c2",
                                    "optionValue": "Unemployed",
                                    "visibilityOrder": null,
                                    "visible": false,
                                    "version": null
                                },
                                {
                                    "id": "2f27f557-4fe0-431a-942a-2f7786f9baec",
                                    "optionValue": "Student",
                                    "visibilityOrder": null,
                                    "visible": false,
                                    "version": null
                                }
                            ]
                        },
                        {
                            "id": "9a04e56c-6857-4d1a-9205-8042d9d77abf",
                            "question": "Annual income (GHS)",
                            "questionType": "SINGLE_CHOICE",
                            "description": null,
                            "visibilityOrder": 3,
                            "identifier": "0aedae9dfb994c0180598d9b9631f37b",
                            "showInGrid": false,
                            "version": 5,
                            "required": true,
                            "kycValue": null,
                            "optionValues": [
                                {
                                    "id": "07aefa92-16c8-48bd-a2cf-3f0b569593db",
                                    "optionValue": "Below 1,000",
                                    "visibilityOrder": null,
                                    "visible": true,
                                    "version": null
                                },
                                {
                                    "id": "c52d2be7-e735-4760-9a7d-95a00e306161",
                                    "optionValue": "1,000 to 10,000",
                                    "visibilityOrder": null,
                                    "visible": true,
                                    "version": null
                                },
                                {
                                    "id": "97523fa3-84b3-4ece-93f9-7fa4a005b420",
                                    "optionValue": "10,001 to 50,000",
                                    "visibilityOrder": null,
                                    "visible": true,
                                    "version": null
                                },
                                {
                                    "id": "76ad8242-778b-4ed5-a00b-00d82a15e19c",
                                    "optionValue": "50,001 to 100,000",
                                    "visibilityOrder": null,
                                    "visible": true,
                                    "version": null
                                },
                                {
                                    "id": "70dc1272-eb10-4d62-bed8-96c8e41e7353",
                                    "optionValue": "Above 100,001",
                                    "visibilityOrder": null,
                                    "visible": true,
                                    "version": null
                                }
                            ]
                        },
                        {
                            "id": "db0b46f4-1f81-4dc7-9f7f-b58f069a3701",
                            "question": "Source of funds",
                            "questionType": "MULTIPLE_CHOICE",
                            "description": null,
                            "visibilityOrder": 4,
                            "identifier": "2f9a1231b1d442fd8e16f0d5044c8f30",
                            "showInGrid": false,
                            "version": 2,
                            "required": true,
                            "kycValue": null,
                            "optionValues": [
                                {
                                    "id": "8e2fc75d-3073-4eb9-91c3-511bde3ad0d3",
                                    "optionValue": "Salary",
                                    "visibilityOrder": null,
                                    "visible": false,
                                    "version": null
                                },
                                {
                                    "id": "25378d0a-c0c6-4a80-a8bd-2bb0f158d32c",
                                    "optionValue": "Personal savings",
                                    "visibilityOrder": null,
                                    "visible": false,
                                    "version": null
                                },
                                {
                                    "id": "4504f795-ad3a-4492-bf22-08650dcecc20",
                                    "optionValue": "Inheritance or gift",
                                    "visibilityOrder": null,
                                    "visible": false,
                                    "version": null
                                },
                                {
                                    "id": "e73aa489-f806-473b-b849-8e606ea7e9d8",
                                    "optionValue": "Proceeds from business",
                                    "visibilityOrder": null,
                                    "visible": false,
                                    "version": null
                                },
                                {
                                    "id": "854a324a-0588-4bf2-b5e7-84d16b816a99",
                                    "optionValue": "Other",
                                    "visibilityOrder": null,
                                    "visible": false,
                                    "version": null
                                }
                            ]
                        }
                    ]
                },
                {
                    "id": "3376c924-b4a4-456d-8b07-3d1943fbff4c",
                    "name": "ID information",
                    "description": null,
                    "visibilityOrder": 3,
                    "identifier": "62be189273624ddb8bca4b034f99e55a",
                    "version": 13,
                    "kycFormQuestions": [
                        {
                            "id": "2c467e3d-70af-48dc-9a3c-eb5707672f02",
                            "question": "Take photo",
                            "questionType": "CAMERA_PHOTO",
                            "description": "Snap to it! Tap and capture your fabulous selfie!",
                            "visibilityOrder": 0,
                            "identifier": "2cf2fa90aa9741c7a1228ed3e9a1c25f",
                            "showInGrid": false,
                            "version": 2,
                            "required": true,
                            "kycValue": null,
                            "optionValues": []
                        },
                        {
                            "id": "658bb167-75ba-437e-b91c-ef99c6f88460",
                            "question": "Upload your Ghana Card",
                            "questionType": "FRONT_PHOTO",
                            "description": "Upload a clear copy of your Ghana Card (max file size:2MB)",
                            "visibilityOrder": 1,
                            "identifier": "ff1e454d275a4c708dcf8b1190e71e3c",
                            "showInGrid": false,
                            "version": 2,
                            "required": true,
                            "kycValue": null,
                            "optionValues": []
                        },
                        {
                            "id": "4ee0a7cb-9418-4c33-85e4-72b0b49d1be5",
                            "question": "Upload your Ghana Card",
                            "questionType": "BACK_PHOTO",
                            "description": "Upload a clear copy of your Ghana Card (max file size:2MB)",
                            "visibilityOrder": 2,
                            "identifier": "72b67399647d4cd795df40053475bda7",
                            "showInGrid": false,
                            "version": 2,
                            "required": true,
                            "kycValue": null,
                            "optionValues": []
                        },
                    ]
                },
                {
                    "id": "5f2dba2c-3839-4b05-bcb0-65e29de09b0e",
                    "name": "Bank Details",
                    "description": null,
                    "visibilityOrder": null,
                    "identifier": "c9cda215465d4c24bafcfe6cba45b608",
                    "version": 11,
                    "kycFormQuestions": [
                        {
                            "id": "a1d6e0be-3560-48aa-892e-f0206b696d1f",
                            "question": "Account name",
                            "questionType": "SINGLE_LINE",
                            "description": null,
                            "visibilityOrder": null,
                            "identifier": "b619569d86884806860d39c7598ca4a1",
                            "showInGrid": false,
                            "version": 1,
                            "required": true,
                            "kycValue": null,
                            "optionValues": []
                        },
                        {
                            "id": "765f69b2-e702-4f42-bb38-a1e7760658f8",
                            "question": "Branch code",
                            "questionType": "NUMERIC",
                            "description": null,
                            "visibilityOrder": null,
                            "identifier": "8b9d46deea774391905985108ca5ed72",
                            "showInGrid": false,
                            "version": 1,
                            "required": true,
                            "kycValue": null,
                            "optionValues": []
                        }
                    ]
                }
            ]
        }
    ]
}
```

### Question Types

Under `kycFormQuestions` each question comes with a `questionType` field that indicates what type of date to collect.

| Type            | Description                                     |
| --------------- | ----------------------------------------------- |
| DATE            | Used to capture date inputs                     |
| MULTI_LINE      | Allows input of multiple lines of text          |
| MULTIPLE_CHOICE | Provides a list of options to choose from       |
| SINGLE_CHOICE   | Allows selection of a single option from a list |
| PHOTO           | Used to upload a photo                          |
| FILE            | Used to upload a file                           |
| CAMERA_PHOTO    | Captures a photo using the device camera        |
| FRONT_PHOTO     | Upload a front-facing photo                     |
| BACK_PHOTO      | Upload a back-facing photo                      |
| PHONE_NUMBER    | Used to input a phone number                    |
| NUMERIC         | Allows input of numeric values only             |
| SINGLE_LINE     | Allows input of a single line of text           |

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
