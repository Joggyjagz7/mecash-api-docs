# meCash API Documentation

## Cross-Border Payment API

### Overview
The POST `/api/v1/payments` endpoint allows users to initiate a cross-border payment between a sender and a recipient. 
With this API, developers can programmatically initiate transactions, validate recipient details, and track payment statuses.

## Request

`POST /api/v1/payments`

### Headers

| Header Name       | Value                        | Description |
|-------------------|----------------------------|-------------|
| `Authorization`   | `Bearer <your_api_key>`     | Your API key for authentication. Replace `<your_api_key>` with your actual key. |
| `Content-Type`    | `application/json`         | Specifies the format of the request body. |

### Body Parameters

The request body must be in JSON format and include the following fields:

| Field                       | Type     | Required | Description |
|-----------------------------|----------|----------|-------------|
| `amount`                    | `number` | Yes      | The amount of money to send, in major units (100.00 for USD). |
| `currency`                  | `string` | Yes      | The currency of the payment (USD for US Dollars). |
| `sender`                    | `object` | Yes      | Information about the person sending the money. |
| `sender.name`               | `string` | Yes      | Full name of the sender (John Doe). |
| `sender.email`              | `string` | Yes      | Email address of the sender (john.doe@x.com). |
| `recipient`                 | `object` | Yes      | Information about the person receiving the money. |
| `recipient.name`            | `string` | Yes      | Full name of the recipient (Jane Smith). |
| `recipient.accountNumber`   | `string` | Yes      | Recipient’s bank account number (0987654321). |
| `recipient.bankCode`        | `string` | Yes      | A code that identifies the recipient’s bank (XYZ456). |
| `recipient.country`         | `string` | Yes      | Recipient’s country (USA). |
| `reference`                 | `string` | Yes      | A unique identifier for the transaction (INV-12345). |

---


## Response

### Success Response (HTTP 201)
If the payment is successful, the server responds with a 201 Created status code and a JSON object containing details about the transaction.

```json
{
  "transactionId": "TXN789456123",
  "status": "SUCCESS",
  "createdAt": "2025-01-12T10:15:30Z",
  "amount": 100.00,
  "currency": "USD",
  "recipient": {
    "name": "Jane Smith",
    "country": "USA"
  }
}
```

Here's what each field means:
| Field | Description |
|-------|-------------|
| **transactionId** | A unique ID for the transaction (e.g., `TXN789456123`). |
| **status** | The status of the transaction. In this case, it’s `SUCCESS`. |
| **createdAt** | The date and time when the transaction was processed (e.g., `2025-01-12T10:15:30Z`). |
| **amount** | The amount of money sent. This is returned in minor units (cents for USD).|
| **currency** | The currency of the payment. |
| **recipient** | An object containing details about the recipient. |
| **recipient.name** | The full name of the recipient. |
| **recipient.country** | The country where the recipient is located. |


#### Error Response (HTTP 400)
If there’s an issue with the request, the server responds with a 400 Bad Request status code and a JSON object explaining the error.

```json
{
  "error": "INVALID_REQUEST",
  "message": "Invalid bank code for the recipient."
}
```


Here’s what each field means:

| Field | Description |
|-------|-------------|
| **error** | A code indicating the type of error (e.g., `INVALID_REQUEST`). |
| **message** | A human-readable message explaining the error `(Invalid bank code for the recipient).` |


#### Other Error Codes and How to Troubleshoot it
Here are some common errors you might encounter:

| HTTP Status Code | Error Code | Description |
|------------------|------------|-------------|
| **400** | `INVALID_REQUEST` | The request is missing required fields or contains invalid data. |
| **401** | `UNAUTHORIZED` | The API key is missing or incorrect or inactive |
| **403** | `FORBIDDEN` | You don’t have permission to perform this transaction. |
| **404** | `NOT_FOUND` | The recipient’s bank or account could not be found. |
| **429** | `RATE_LIMIT_EXCEEDED` |  Too many requests. Slow down your API calls. |
| **500** | `INTERNAL_ERROR` | Something went wrong on the server. Contact support |

--- 


### Code Examples

#### cURL Example
```cURL
curl -X POST https://api.mecash.com/api/v1/payments \
-H "Authorization: Bearer your_api_key" \
-H "Content-Type: application/json" \
-d '{
  "amount": 100.00,
  "currency": "USD",
  "sender": {
    "name": "John Doe",
    "email": "john.doe@x.com"
  },
  "recipient": {
    "name": "Jane Smith",
    "accountNumber": "0987654321",
    "bankCode": "XYZ456",
    "country": "USA"
  },
  "reference": "INV-12345"
}'
```

#### Python Example
```Python

import requests

url = "https://api.mecash.com/api/v1/payments"
headers = {
    "Authorization": "Bearer your_api_key",
    "Content-Type": "application/json"
}

payload = {
    "amount": 100.00,
    "currency": "USD",
    "sender": {
        "name": "John Doe",
        "email": "john.doe@x.com"
    },
    "recipient": {
        "name": "Jane Smith",
        "accountNumber": "0987654321",
        "bankCode": "XYZ456",
        "country": "USA"
    },
    "reference": "INV-12345"
}

response = requests.post(url, json=payload, headers=headers)
print(response.json())
```
----

### Additional Notes
- Transactions typically process within 30 seconds.
- Ensure all requests are idempotent by using a unique reference field.
- You can test the API using Postman or Swagger UI.

For further assistance, visit the meCash API Developer Portal.


