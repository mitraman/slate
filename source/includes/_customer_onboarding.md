# Customer On-boarding

Use this endpoint to create and manage applications for new customers

## Initiate onboarding

```shell
curl "http://example.com/api/accounts/22289/balance" \
  -H "Authorization: Bearer token"
```

> The above command returns a list of accounts as an array:

```json
HTTP 200 OK

{
  "Balances": [
      {
        "AccountId": "22289",
        "Amount": {
          "Amount": "1230.00",
          "Currency": "GBP"
        },
        "CreditDebitIndicator": "Credit",
        "Type": "InterimAvailable",
        "DateTime": "2017-04-05T10:43:07+00:00",
        "CreditLine": [
          {
            "Included": true,
            "Amount": {
              "Amount": "1000.00",
              "Currency": "GBP"
            },
            "Type": "Pre-Agreed"
          }
        ]
      }
    ] 
}
```

> If the bank account that has been specified cannot be retrieved, the API will return a 404 error message:

```json
HTTP 404 NOT FOUND

{
  "Accounts" : []    
}
```

This endpoint retrieves a list of bank accounts for an authenticated user. Every item in the resulting array is a complete representation of an account (i.e. there is no need to make a subsequent GET call to retrieve additional account information details.)

### HTTP Request

`GET http://example.com/api/accounts/{AccountID}/balance`

## Submit application

```shell
curl "http://example.com/api/balances" \
  -H "Authorization: Bearer token"
```

> The above command returns an array of balances for all bank accounts associated with the signed in user

```json
{
  "Balances" : [
      {
        "AccountId": "22289",
        "Amount": {
          "Amount": "1230.00",
          "Currency": "GBP"
        },
        "CreditDebitIndicator": "Credit",
        "Type": "InterimAvailable",
        "DateTime": "2017-04-05T10:43:07+00:00",
        "CreditLine": [
          {
            "Included": true,
            "Amount": {
              "Amount": "1000.00",
              "Currency": "GBP"
            },
            "Type": "Pre-Agreed"
          }
        ]
      },
      {
        "AccountId": "31820",
        "Amount": {
          "Amount": "57.36",
          "Currency": "GBP"
        },
        "CreditDebitIndicator": "Debit",
        "Type": "InterimBooked",
        "DateTime": "2017-05-02T14:22:09+00:00"
      }
    ] 
}
```

This endpoint retrieves the bank account identified in the URI

### HTTP Request

`GET http://example.com/api/balances`
