# Calculate Maturity Amount and Estimate Interest

#### Endpoint
**POST** `/api/client/{clientId}/portfolio/{portfolioId}/product/{productId}/consideration`

**URL Example:**
```
https://api.portal.uatdev.blackstargroup.ai/api/client/{clientId}/portfolio/{portfolioId}/product/{securityId}/consideration?date={issueDate}
```

#### Description
This endpoint is used to calculate maturity amount for a consideration for a specific security within a portfolio.

#### Query Parameters
- **date**: `string`  
  The issue date of the security in `DD-MM-YYYY` format.

#### Request Body
The request body should be a JSON object with the following fields:

| Field          | Type     | Description                                               |
|----------------|----------|-----------------------------------------------------------|
| `yield`        | `number` | The yield percentage of the consideration (for COMPETITIVE bids).                |
| `orderSide`    | `string` | The side of the order (should always be "BUY").             |
| `consideration`| `number` | The amount to be considered for the order.                |
| `currencyCode` | `string` | The currency code, e.g., "GHS".                           |
| `orderOfferId` | `string` | The unique identifier for the order offer.                |

**Example Request Body:**
```json
{
  "yield": 24,
  "orderSide": "BUY",
  "consideration": 100,
  "currencyCode": "GHS",
  "orderOfferId": "1981d8b9-3962-4048-a580-64e313b18377"
}
```

#### Response
The API will return a JSON response indicating the result of the consideration submission.

#### Example cURL Command
```bash
curl -X 'POST' \
  'https://api.portal.uatdev.blackstargroup.ai/api/client/64938179-0dec-asdd-ba26-8e0ea2b37aa3/portfolio/8a208c43-a6a3-4abe-9b36-7339c3c68a53/product/6edd9552-acfd-4646-aa7f-b53d9365e520/consideration?date=02-09-2024' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer {token}' \
  -H 'Content-Type: application/json' \
  -d '{
  "yield": 24,
  "orderSide": "BUY",
  "consideration": 100,
  "currencyCode": "GHS",
  "orderOfferId": "1981d8b9-3962-4048-a580-64e313b18377"
}'
```
