# Hypermedia Accounts

Use the `accounts` endpoint to work with bank accounts associated with an authenticated user.

## Accounts Data Model

## Link Relations

### self

### statements

```
"ps:statements": { "href": "https://api.publicissapient.com/accountstatements" }
```

`https://api.publicissapient.com/rels/statements`

The rel `statements` indicates a link can be followed to retrieve a specific account's statements data. Making a GET request for this type of link will return a statements response.

### balances

```
"ps:balances": { "href": "https://api.publicissapient.com/accounts/2232/balance" }
```

`https://api.publicissapient.com/rels/balances`

The rel `balances` indicates that a link can be followed to retrieve a specific account's balances data or balances data for all of a customer's accounts. Making a GET request for this type of link will return a balances response. 

### features


## Retrieve a List of Accounts

```shell
curl "http://example.com/api/accounts" \
  -H "Authorization: Bearer token"
```

> The above command returns a list of accounts as an array:

```json
HTTP 200 OK
application/hal+json

{ 
  "_links": {
    "self": { "href": "http://api.publicissapient.com/baas/accounts" },
    "curie": {
      "name": "ps",
      "href": "https://api.publicissapient.com/rels/{rel}",
      "templated": true
    },
    "ps:balances": { "href": "http://api.publicissapient.com/baas/balances" },
  },
  "_embedded": {
    "Accounts" : [
    {
        "_links": {
          "self": { "href": "http://api.publicissapient.com/baas/accounts/22289" },          
          "ps:statements": { "href": "http://api.publicissapient.com/baas/accounts/22289/statements" },
          "ps:balances": { "href": "http://api.publicissapient.com/baas/accounts/22289/balances" },
          "ps:features": { "href": "http://api.publicissapient.com/baas/product/personal_current_1"}
        },
        "AccountId": "22289",
        "Status": "Enabled",
        "StatusUpdateDateTime": "2019-01-01T06:06:06+00:00",
        "Currency": "GBP",
        "AccountType": "Personal",
        "AccountSubType": "CurrentAccount",
        "Nickname": "Bills",
        "Account": [
            {
                "IdentifierType": "IBAN",
                "Identifier": "AE070331234567890123456",
                "Name": "Mr Kevin",
                "SecondaryIdentification": "00021"
            }
        ]
    },
    {
        "_links": {
          "self": { "href": "http://api.publicissapient.com/baas/accounts/31820" },          
          "ps:statements": { "href": "http://api.publicissapient.com/baas/accounts/31820/statements" },
          "ps:balances": { "href": "http://api.publicissapient.com/baas/accounts/31820/balances" },
          "ps:features": { "href": "http://api.publicissapient.com/baas/product/personal_current_1"}
        },
        "AccountId": "31820",
        "Status": "Enabled",
        "StatusUpdateDateTime": "2018-01-01T06:06:06+00:00",
        "Currency": "GBP",
        "AccountType": "Personal",
        "AccountSubType": "CurrentAccount",
        "Nickname": "Household",
        "Account": [
            {
                "IdentifierType": "SortCode",
                "Identifier": "80200110203348",
                "Name": "Mr Kevin"
            }
        ]
    }
    ]    
}
}
```

> If there are no bank accounts associated with the authenticated user, an empty Accounts array is returned:

```json
HTTP 200 OK

{
  "Accounts" : []    
}
```

> By default, balances are not included in the Account's representation, however if the request parameter `include=balances` is set, balances will be included as a child property of each account object:

```json
HTTP 200 OK

{
  "Accounts" : [
        {
            "AccountId": "22289",
            "Status": "Enabled",
            "StatusUpdateDateTime": "2019-01-01T06:06:06+00:00",
            "Currency": "GBP",
            "AccountType": "Personal",
            "AccountSubType": "CurrentAccount",
            "Nickname": "Bills",
            "Account": [
                {
                    "IdentifierType": "IBAN",
                    "Identifier": "AE070331234567890123456",
                    "Name": "Mr Kevin",
                    "SecondaryIdentification": "00021"
                }
            ],
            "Balances": [
              {
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
        },
        {
            "AccountId": "31820",
            "Status": "Enabled",
            "StatusUpdateDateTime": "2018-01-01T06:06:06+00:00",
            "Currency": "GBP",
            "AccountType": "Personal",
            "AccountSubType": "CurrentAccount",
            "Nickname": "Household",
            "Account": [
                {
                    "SchemeName": "SortCode",
                    "Identifier": "80200110203348",
                    "Name": "Mr Kevin"
                }
            ],
            "Balances": [
              {
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
    ]    
}
```



This endpoint retrieves a list of bank accounts for an authenticated user. 

### HTTP Request

`GET http://example.com/api/accounts`

## Retrieve a Specific Account

```shell
curl "http://example.com/api/accounts/31820" \
  -H "Authorization: Bearer token"
```

> The above command returns an Accounts array with the identified account as the only item.

```json
{
  "Accounts" : [        
        {
            "AccountId": "31820",
            "Status": "Enabled",
            "StatusUpdateDateTime": "2018-01-01T06:06:06+00:00",
            "Currency": "GBP",
            "AccountType": "Personal",
            "AccountSubType": "CurrentAccount",
            "Nickname": "Household",
            "Account": [
                {
                    "SchemeName": "UK.OBIE.SortCodeAccountNumber",
                    "Identification": "80200110203348",
                    "Name": "Mr Kevin"
                }
            ]
        }
    ]    
}
```

This endpoint retrieves the bank account identified in the URI

### HTTP Request

`GET http://example.com/api/accounts/{AccountId}`
