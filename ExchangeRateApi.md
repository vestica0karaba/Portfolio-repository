# Currency Exchange Rate API - Receive Real Time Rates

This API allows users to retrieve real-time exchange rates for different currencies. 

## Endpoint: Request API

## Getting Started

**URL:**

https://api.exchangerate-api.com/v4/latest/USD

**Method:** "GET"

1. **Sign up for an API key**:
	-Go to [ExchangeRate API](https://www.exchangerate-api.com/) and sign up for a free API key.

2. **Make the request**:
	-After you obtained the key, to fetch the exchange rates for **USD**, send the following request:
	
	GET https://api.exchangerate-api.com/v4/latest/USD


**Authentication:** Not required for free-tier users.


### Headers

|Header       |Description                       |Required |
|-------------|----------------------------------|---------|
|Content-Type |The format of the request payload |No       |
|Accept       |Type format of the response       |No       |


### Parameters

|Parameter     |Type    |Required  |Description                  |
|--------------|--------|----------|-----------------------------|
|"base_curency"|string  |Yes       | The base curency you request|


### Example Request

To fetch the exchange rates for **USD**, send the following request:

GET https://api.exchangerate-api.com/v4/latest/USD


### Headers

{
	"Accept": "application/json",
	"Content-Type": "application/json"
}	


### Example responses:

{
  "base": "USD",
  "date": "2025-03-13",
  "rates": {
    "EUR": 0.92,
    "GBP": 0.78,
    "JPY": 150.32,
    "CAD": 1.35
  }
}


### Response Format

The response from the API will be in **JSON** format and contains the following key elements:

|Key         |Type     |Description                                                  |
|------------|---------|-------------------------------------------------------------|
|"base"      |string   |The base currency used for the exchange rates (e.g., "USD")  |
|"date"      |string   |The date the exchange rates were last updated                |
|"rates"     |object   |An object containing exchange rates for various currencies   |


### "rates" Objects

|Currency Code |Type   |Description                                          |
|--------------|-------|-----------------------------------------------------|
|"EUR"         |number |The exchange rate for EUR against the base currency. |
|"GBP"         |number |The exchange rate for BGP against the base currency. |
|"JPY"         |number |The exchange rate for JPY against the base currency. |
|"CAD"         |number |The exchange rate for CAD against the base currency. |

### Status and Errors

|Code                        |Description                                          |
|----------------------------|-----------------------------------------------------|
|"200 OK"                    |Successfully retreived data                          |
|"400 Bad Request"           |Invalid or missing currency code                     |
|"404 Not Found"             |API endpoint not found                               |
|"429 Too Many Requests"     |Rate limit exceeded                                  |
|"500 Internal Server Error" |An error occurred processing the request on a server |


### Error Messages 

|Code                        |Cause                                                     |Fix                                                                            |
|----------------------------|----------------------------------------------------------|-------------------------------------------------------------------------------|
|"400 Bad Request"           |The request was malformed or missing required parameters. |Check the request URL for correctness and ensure the `base_currency` is valid. |
|"404 Not Found"             |The API endpoint or resource was not found.               |Ensure the URL endpoint is correct.                                            |
|"429 Too Many Requests"     |You have exceeded the rate limit for API requests.        |Wait for the rate limit to reset.                                              |
|"500 Internal Server Error" |The server encountered an unexpected error.               |Try again later. If the issue persists, contact support.                       |


## Code Sample

### Python Example:

import requests

url = "https://api.exchangerate-api.com/v4/latest/USD"

response = requests.get(url)

if response.status_code == 200:
    data = response.json()
    print("Exchange rate for EUR:", data["rates"]["EUR"])
else:
    print("Error:", response.status_code)
