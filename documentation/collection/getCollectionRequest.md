# Get All Collection Requests

## Overview

This API endpoint is used to retrieve all collection requests based on a client or portfolio.

### Endpoint

```
POST /api/client/{clientId}/collectionRequest/search
```

### Parameters

| Name        | Type    | Description     | Required | In    |
| ----------- | ------- | --------------- | -------- | ----- |
| clientId    | string  | Client UUID     | Yes      | path  |
| portfolioId | string  | Portfolio UUID  | No       | query |
| page        | integer | Current page    | Yes      | query |
| size        | integer | Maximum records | Yes      | query |

### Request Body

| Name        | Type    | Description                   | Required |
| ----------- | ------- | ----------------------------- | -------- |
| startDate   | string  | Start date in ISO 8601 format | No       |
| endDate     | string  | End date in ISO 8601 format   | No       |
| status      | string  | Status of the request         | No       |
| year        | integer | Year                          | No       |
| requestType | string  | Type of request               | No       |
| custodianId | string  | Custodian UUID                | No       |

#### Example Request Body

```json
{
  "startDate": "2024-07-02T10:40:06.799Z",
  "endDate": "2024-07-02T10:40:06.799Z",
  "status": "SUBMITTED",
  "year": 0,
  "requestType": "COLLECTION",
  "custodianId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

### Responses

#### 200 OK

| Name             | Type    | Description                        |
| ---------------- | ------- | ---------------------------------- |
| totalElements    | integer | Total number of elements           |
| totalPages       | integer | Total number of pages              |
| size             | integer | Number of records per page         |
| content          | array   | List of collection requests        |
| number           | integer | Current page number                |
| sort             | object  | Sorting information                |
| numberOfElements | integer | Number of elements on current page |
| pageable         | object  | Pageable information               |
| first            | boolean | Is this the first page?            |
| last             | boolean | Is this the last page?             |
| empty            | boolean | Is the content empty?              |

##### Example Response Body

```json
{
  "totalElements": 0,
  "totalPages": 0,
  "size": 0,
  "content": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "portfolioId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "portfolioName": "string",
      "hubtleConfigId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "amount": 0,
      "transactionId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "requestType": "COLLECTION",
      "status": "SUBMITTED",
      "executionErrorMessage": "string",
      "description": "string",
      "valueDate": "2024-07-02T10:40:06.800Z",
      "custodianId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
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

### Example Code

#### CURL

```sh
curl -X POST "https://api.example.com/api/client/3fa85f64-5717-4562-b3fc-2c963f66afa6/collectionRequest/search?page=0&size=10" \
-H "Content-Type: application/json" \
-d '{
  "startDate": "2024-07-02T10:40:06.799Z",
  "endDate": "2024-07-02T10:40:06.799Z",
  "status": "SUBMITTED",
  "year": 0,
  "requestType": "COLLECTION",
  "custodianId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}'
```

#### JavaScript (Axios)

```javascript
const axios = require("axios");

const data = {
  startDate: "2024-07-02T10:40:06.799Z",
  endDate: "2024-07-02T10:40:06.799Z",
  status: "SUBMITTED",
  year: 0,
  requestType: "COLLECTION",
  custodianId: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
};

axios
  .post(
    "https://api.example.com/api/client/3fa85f64-5717-4562-b3fc-2c963f66afa6/collectionRequest/search?page=0&size=10",
    data,
    {
      headers: {
        "Content-Type": "application/json",
      },
    }
  )
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

### Notes

- Ensure the `clientId` parameter in the path is a valid UUID.
- Pagination parameters `page` and `size` are mandatory.
- The request body parameters such as `startDate`, `endDate`, `status`, `year`, `requestType`, and `custodianId` are optional but can be used to filter the collection requests.
- The response contains pagination details and a list of collection requests matching the criteria.
