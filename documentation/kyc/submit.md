# Submit KYC

Submits a Know Your Customer (KYC) application for review.

> **New** 📢
> You can now add a webhook for KYC status updates
> When submitting KYC, you can include a webhook URL in the request body

## Endpoint Details

- **URL:** `/api/kyc/{kycId}/submit`
- **Method:** PUT
- **Description:** Submit KYC for review

## Request

### Parameters

| Name  | Located In | Description                               | Required | Schema        |
| ----- | ---------- | ----------------------------------------- | -------- | ------------- |
| kycId | path       | Unique identifier for the KYC application | Yes      | string (UUID) |

### Request Body

| Name       | Type   | Required | Description                                        |
| ---------- | ------ | -------- | -------------------------------------------------- |
| webhookUrl | string | Yes      | Webhook URL to be notified when KYC status changes |

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
  "name": "string", // [ VERIFIED, REJECTED, PENDING, SUBMITTED ]
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
  "clientSubTypeUUID": "string",
  "clientSubTypeName": "string",
  "currentSectionIdentifier": "string",
  "portfolioId": "string",
  "clientId": "string"
}
```

### Webhook Data

```json
{
  "eventType": "KYC_STATUS",
  "kycID": "string",
  "timeStamp": "07-03-2025 09:23",
  "kycStatus": "VERIFIED", // [ VERIFIED, REJECTED, PENDING, SUBMITTED ]
  "rejectionReason": null,
  "clientSubTypeUUID": "string",
  "portfolioId": "string",
  "clientId": "string"
}
```

Once the KYC is verified or rejected, we will send the status update to the provided webhook URL.

Additionally, please ensure that our production IP `(18.102.87.24)` is whitelisted on the API receiving the webhook. This will help prevent unauthorized messages from being pushed to it.

Upon verification, we will send an immediate webhook response. If the first attempt fails, we will retry after 5-10 minutes, followed by a second retry after another 5-10 minutes. In total, we will make up to three retry attempts.

## Example Usage

### Javascript

```javascript
const axios = require("axios");

// Replace with your API base URL
const baseUrl = "https://api.uatdev.blackstargroup.ai";

// Replace with an actual KYC ID
const kycId = "KYC_ID";

const url = `${baseUrl}/api/kyc/${kycId}/submit`;

const headers = {
  Authorization: "Bearer YOUR_ACCESS_TOKEN",
};

axios
  .put(
    url,
    {
      webhookUrl: "WEBHOOK_URL_HERE",
    },
    { headers }
  )
  .then((response) => {
    console.log("KYC submitted successfully:");
    console.log(`KYC ID: ${response.data.id}`);
    console.log(`Status: ${response.data.kycStatus}`);
  })
  .catch((error) => {
    console.error(`Error submitting KYC: ${error.response?.status}`);
    console.error(error.response?.data);
  });
```

## Notes

- Ensure that you replace `YOUR_ACCESS_TOKEN` with a valid authentication token.
- The `kycId` in the URL should be a valid UUID of an existing KYC application.
- The response includes detailed information about the submitted KYC, including user answers, form structure, and current status.
- Handle potential errors by checking the response status code and the `errorMessage` field in the response body.
