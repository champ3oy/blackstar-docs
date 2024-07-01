# Get All UserKYC API

**Endpoint:** POST /api/kyc/get/all

**Description:** Retrieves all UserKYC records with optional filtering and pagination.

## Request

### Query Parameters:

- `page` (required, integer): Page number for pagination
- `size` (required, integer): Number of results per page

### Request Body:

```json
{
  "kycStatusList": ["VERIFIED"],
  "kycConfigUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "searchQuery": "string",
  "startDate": "2024-06-28T13:21:56.556Z",
  "endDate": "2024-06-28T13:21:56.556Z"
}
```

- `kycStatusList` (array of strings): List of KYC statuses to filter by
- `kycConfigUUID` (string, UUID): UUID of the KYC configuration to filter by
- `searchQuery` (string): Search term to filter results
- `startDate` (string, date-time): Start date for filtering results
- `endDate` (string, date-time): End date for filtering results

## Response

### Status Code: 200 OK

### Response Body:

```json
{
  "totalPages": 0,
  "totalElements": 0,
  "size": 0,
  "content": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "userId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "updatedOn": "2024-06-28T13:21:56.560Z",
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
  ],
  "number": 0,
  "sort": {
    "empty": true,
    "sorted": true,
    "unsorted": true
  },
  "numberOfElements": 0,
  "pageable": {
    "offset": 0,
    "sort": {
      "empty": true,
      "sorted": true,
      "unsorted": true
    },
    "pageSize": 0,
    "pageNumber": 0,
    "paged": true,
    "unpaged": true
  },
  "first": true,
  "last": true,
  "empty": true
}
```

### Response Fields:

- `totalPages` (integer): Total number of pages
- `totalElements` (integer): Total number of elements across all pages
- `size` (integer): Number of elements in the current page
- `content` (array): List of UserKYC objects
  - `id` (string, UUID): Unique identifier for the UserKYC record
  - `userId` (string, UUID): Unique identifier for the user
  - `updatedOn` (string, date-time): Last update timestamp
  - `kycStatus` (string): Current KYC status (e.g., "VERIFIED")
  - `name` (string): User's name
  - `userKYCAnswerList` (array): List of user's KYC answers
  - `kycFormDTO` (object): KYC form structure and details
  - `errorMessage` (string): Any error message associated with the KYC process
  - `email` (string): User's email
  - `phone` (string): User's phone number
  - `rejectionReason` (string): Reason for KYC rejection, if applicable
  - `currentSectionIdentifier` (string): Identifier of the current KYC section
- `number` (integer): Current page number
- `sort` (object): Sorting information
- `numberOfElements` (integer): Number of elements in the current page
- `pageable` (object): Pagination information
- `first` (boolean): Indicates if this is the first page
- `last` (boolean): Indicates if this is the last page
- `empty` (boolean): Indicates if the result set is empty

# Example Code

## cURL

```bash
curl -X POST 'https://api.example.com/api/kyc/get/all?page=1&size=10' \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
-d '{
  "kycStatusList": ["VERIFIED"],
  "kycConfigUUID": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "searchQuery": "John Doe",
  "startDate": "2024-01-01T00:00:00.000Z",
  "endDate": "2024-06-28T23:59:59.999Z"
}'
```

Replace `https://api.example.com` with your actual API base URL and `YOUR_ACCESS_TOKEN` with a valid access token.

## JavaScript (Axios)

```javascript
const axios = require("axios");

async function getAllUserKYC() {
  try {
    const response = await axios({
      method: "post",
      url: "https://api.example.com/api/kyc/get/all",
      params: {
        page: 1,
        size: 10,
      },
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer YOUR_ACCESS_TOKEN",
      },
      data: {
        kycStatusList: ["VERIFIED"],
        kycConfigUUID: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        searchQuery: "John Doe",
        startDate: "2024-01-01T00:00:00.000Z",
        endDate: "2024-06-28T23:59:59.999Z",
      },
    });

    console.log("Total Pages:", response.data.totalPages);
    console.log("Total Elements:", response.data.totalElements);
    console.log("KYC Records:", response.data.content);

    // Process the KYC records
    response.data.content.forEach((record) => {
      console.log(`User: ${record.name}, KYC Status: ${record.kycStatus}`);
    });
  } catch (error) {
    console.error(
      "Error fetching KYC data:",
      error.response ? error.response.data : error.message
    );
  }
}

getAllUserKYC();
```

Remember to replace `https://api.example.com` with your actual API base URL and `YOUR_ACCESS_TOKEN` with a valid access token.

### Notes on the JavaScript example:

1. This example uses async/await for cleaner asynchronous code.
2. The query parameters (`page` and `size`) are passed in the `params` object.
3. The request body is passed in the `data` object.
4. The example includes basic error handling and logging of the response data.
5. It demonstrates how to access and process the paginated KYC records from the response.

To use this in a browser environment, you may need to use a module bundler like webpack or include Axios via a CDN. Also, make sure to handle any CORS (Cross-Origin Resource Sharing) issues that may arise when making requests from a browser to your API.

These examples should help you get started with integrating this API endpoint into your application. Remember to adjust the URL, headers, and request body according to your specific API configuration and use case.

## Notes:

1. This API supports pagination and filtering, allowing for efficient retrieval of large datasets.
2. The `kycStatusList` in the request body allows filtering by multiple KYC statuses.
3. The `searchQuery` parameter can be used for general search across relevant fields.
4. Date range filtering is possible using `startDate` and `endDate`.
5. The response includes detailed information about each user's KYC submission, including their answers and the associated form structure.
6. The `kycFormDTO` in the response provides the complete structure of the KYC form, including sections, subsections, and questions.
7. Pagination metadata in the response allows for easy implementation of paginated interfaces.
8. The API returns a 200 OK status for successful requests, even if the result set is empty.

This API is designed to provide comprehensive KYC information with flexible querying options, making it suitable for administrative interfaces and reporting tools in KYC management systems.
