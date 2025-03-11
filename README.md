> **Important**
> **This a sample Banking API Document. It is not used for any operation.**

# Bank API Documentation 

The Bank API provides information about authentication, checking balance, checking transaction history, and initiating fund transfer activities.
This documentation provides information about each endpoint in the API with their examples requests and responses in JSON and C#. 
> JSON and C# responses are provided in separate dropdowns. If no dropdown is present, the response in the code block is in JSON format. 

#### Contents

## Overview
Bank’s API is a JSON and C# based OAuth2 API. All requests are made to endpoints beginning:

`https://api.medium.com/v1`

All requests are served over `HTTPS`. To ensure data privacy, unencrypted `HTTP` is not supported.

## 2. Authentication

All requests require an API key for authentication. The API accepts HTTP basic authentication for some endpoints and OAuth authentication for all endpoints.

#### a) Basic Authentication 

```
GET /accounts

Authorization: Bearer YOUR_API_KEY

The API accepts HTTP basic authentication (also known as basic authentication) for some endpoints that do not access specific customer information. Follow these steps to use basic authentication:

curl -X GET --user 123abc456def:1a2b3c4d \
"https://api.shutterstock.com/v2/images/search" \
  -G \
  --data-urlencode "query=sunrise"
Create an account at https://www.shutterstock.com if you don't already have one.
Set up an application at https://www.shutterstock.com/account/developers/apps and get the consumer key and consumer secret from the application.
Pass the consumer key and consumer secret to the API along with the request. For example, you can use basic authentication to search for images by using the GET /v2/images/search endpoint. The example in the right-hand pane passes the ID and secret (in this case, 123abc456def and 1a2b3c4d) in place of a user name and password.
API endpoints that require an OAuth scope do not accept basic authentication. To use these endpoints, you must use OAuth authentication.


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

<details>
  <summary>Languages</summary>
  
  <details>
    <summary>Python</summary>
    
    Python is a popular programming language.

  </details>

  <details>
    <summary>Java</summary>
    
    Java is widely used in enterprise applications.

  </details>

</details>

