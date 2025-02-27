# meCash Cross-Border Payments API Documentation  

## Overview  

This repository contains the API documentation for the meCash cross-border payments system. It provides developers with detailed guidance on integrating with the `POST /api/v1/payments` endpoint, including request structure, response formats, error handling, and example implementations.  It contains the following:
- **Clear API Reference** – Covers request parameters, headers, and response formats.  
- **Error Handling Guide** – Details common errors and troubleshooting tips.  
- **Code Examples** – Provides sample API requests and responses.


## Getting Started

To access the full API documentation, open the [`API_Documentation.md`](API_Documentation.md) file. 

It can also be viewed locally by cloning this repository to your local machine using the following command:
```https
git clone (https://github.com/Joggyjagz7/mecash-api-docs.git)
```
Navigate to the cloned folder after the cloning process is complete
```https
cd mecash-api-docs
```
Open API_Documentation.md in a Markdown viewer or editor like VS Code.

### Prerequisites

Before making API requests, ensure you have:

- meCash API key (obtainable from meCash Developer Portal).
- A development environment with tools like Postman or cURL.
- Basic knowledge of JSON formatting.

### Base URL

All API requests should be directed to:
```https
https://api.mecash.com/api/v1
```


## Making a Request  

Use the following cURL command to initiate a cross-border payment:  

```bash
curl -X POST https://api.mecash.com/api/v1/payments \
  -H "Authorization: Bearer YOUR_API_KEY" \
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


## Contributing
Contributions are welcome! If you find any issues or have suggestions, feel free to open a pull request or submit an issue.


## Support
For questions or assistance, contact meCash Developer Support at support@mecash.com.


## License
This project is licensed under MIT License.
