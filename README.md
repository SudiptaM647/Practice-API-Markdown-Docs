> **Important**
> This a sample Banking API Document for practicing Marckdown and API Documentation methods. It is not used for any operation.

# Bank API Documentation 

The Bank API provides information about authentication, checking balance, checking transaction history, and initiating fund transfer activities.
This documentation provides information about each endpoint in the API with their examples requests and responses in JSON and C#. 
> JSON and C# responses are provided in separate dropdowns. If no dropdown is present, the response in the code block is in JSON format. 

#### Contents

## Overview
Bank’s API is a `JSON` and `C#` based `OAuth2 API`. All requests are made to endpoints beginning:

`https://api.medium.com/v2`

All requests are served over `HTTPS`. To ensure data privacy, unencrypted `HTTP` is not supported.

## 2. Authentication

All requests require an API key for authentication. The API accepts HTTP basic authentication for some endpoints and OAuth authentication for all endpoints.

#### a) Basic Authentication 

```
GET /accounts

Authorization: Bearer YOUR_API_KEY
```
#### b) Query Parameter Authentication
```
GET /accounts?api_key=YOUR_API_KEY
```
### Authentication Error Response
If authentication fails, you receive:
```
{
  "error": {
    "code": 401,
    "message": "Invalid API key. Please provide a valid key."
  }
}
```

## 3. Endpoints

### Get Account Balance
You can check the account balance using the following endpoint:

```
GET /v2/accounts/{account_id}/balance
```
**Request Parameter**

| Parameter       | Type     | Required?  | Description                                     |
| -------------   |----------|------------|-------------------------------------------------|
| `account_id`     | string   | required   | The unique identifier for the bank account. |

#### Request Methods
The following example represents `cURL` and `Node.js` request methods. 
<details>
  <summary>Request Methods</summary>
  
  <details>
    <summary>cURL</summary>
    
    curl -X GET "https://api.banksecure.com/v2/accounts/123456789/balance" \
     -H "Authorization: Bearer YOUR_API_KEY" \
     -H "Content-Type: application/json"

  </details>

  <details>
    <summary>Node.js</summary>
    
    const axios = require('axios');

    axios.get('https://api.banksecure.com/v2/accounts/123456789/balance', {
      headers: { Authorization: 'Bearer YOUR_API_KEY' }
      })
    .then(response => console.log(response.data))
    .catch(error => console.error(error));

  </details>
</details>

#### Success Response
For successful request, you will receive a success response. The following example covers `JSON` and `C#` examples.

<details>
  <summary>Success Requests</summary>
  
  <details>
    <summary>JSON Response</summary>
    
    const axios = require('axios');

    axios.get('https://api.banksecure.com/v2/accounts/123456789/balance', {
    headers: { Authorization: 'Bearer YOUR_API_KEY' }
    })
    .then(response => console.log(response.data))
    .catch(error => console.error(error));

  </details>
  <details>
    <summary>C# Response</summary>
    
    public class AccountBalanceResponse
{
    public string AccountId { get; set; }
    public decimal Balance { get; set; }
    public string Currency { get; set; }
}
  </details>
</details>

### Fund Transfer
Transfer funds between two bank accoutns using the following endpoint:
```
POST /v2/accounts/{account_id}/transfer
```
**Request Parameter**

| Parameter       | Type     | Required?  | Description                                     |
| -------------   |----------|------------|-------------------------------------------------|
| `account_id`    | string   | required   | The unique identifier for the sender bank account. |
| `recipient_id`  | string   | required   | The unique identifier for the recipient bank account. |
| `amount`  | decimal   | required   | The value of transfer amount. |
| `currency`  | string   | required   | The currency of the transaction. |

#### Request Methods
The following example represents `cURL` and `Node.js` request methods. 
<details>
  <summary>Request Methods</summary>
  
  <details>
    <summary>cURL</summary>
    
    curl -X POST "https://api.banksecure.com/v2/accounts/123456789/transfer" \
     -H "Authorization: Bearer YOUR_API_KEY" \
     -H "Content-Type: application/json" \
     -d '{
           "recipient_id": "987654321",
           "amount": 500.00,
           "currency": "USD"
         }'

  </details>

  <details>
    <summary>Node.js</summary>
    
    const axios = require('axios');

    axios.post('https://api.banksecure.com/v2/accounts/123456789/transfer', {
    recipient_id: "987654321",
    amount: 500.00,
    currency: "USD"
    }, {
    headers: { Authorization: 'Bearer YOUR_API_KEY' }
    })
    .then(response => console.log(response.data))
    .catch(error => console.error(error));
  </details>
  
</details>

#### Success Response
For successful request, you will receive a success response.

<details>
  <summary>Success Requests</summary>
  
  <details>
    <summary>JSON Response</summary>
    
    {
    "transaction_id": "TRX123456",
    "status": "Success",
    "amount": 500.00,
    "currency": "USD",
    "timestamp": "2025-03-04T10:15:30Z"
    }

  </details>
  <details>
    <summary>C# Response</summary>
    
   public class TransferResponse
{
    public string TransactionId { get; set; }
    public string Status { get; set; }
    public decimal Amount { get; set; }
    public string Currency { get; set; }
    public DateTime Timestamp { get; set; }
}
  </details>
</details>

## 4. Error Response 
The API returns error codes along with information about the error. Here are some common error responses:

| Error code  | Error Message           | Description                                     |
| ------------|-------------------------|-------------------------------------------------|
| 400         | `Invalid request`       |The request contains invalid `parameters`.       |
| 401         | `Unauthorized`          |The API key is missing or invalid.               |
| 403         | `Forbidden`             |The user doesn’t have permission.                |
| 404         | `Account Not Fount`     |The specified account ID doesn’t exist.          |
| 429         | `Rate Limit Exceeded`   |Too many requests in a short period.             |
| 500         | `Internal Server Error` |A problem occurred on the bank's server.         |

Some examples of error responses:

<details>
  <summary>Error Responses</summary>
  
  <details>
    <summary>JSON</summary>
    
    {
    "error": {
    "code": 400,
    "message": "Invalid request. Please check your parameters."
    }
    }
  </details>

  <details>
    <summary>C#</summary>
public class ErrorResponse
{
    public int Code { get; set; }
    public string Message { get; set; }
}
  </details>
  
</details>

## 5. Release notes

**2025-01-14 (v2.1.0)**
Removed the following unused endpoints due to service deprecation:
```
GET https://api.banksecure.com/v1/accounts/
```
