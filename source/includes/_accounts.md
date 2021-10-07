# Accounts

Use the `accounts` endpoint to work with bank accounts associated with an authenticated user.

## Accounts Data Model


## Retrieve a List of Accounts

```shell
curl "http://example.com/api/accounts" \
  -H "Authorization: Bearer token"
```

> The above command returns a list of accounts as an array:

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
                    "IdentifierType": "SortCode",
                    "Identifier": "80200110203348",
                    "Name": "Mr Kevin"
                }
            ]
        }
    ]    
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

## Accounts Events


### Account Open Initiated

```
{
  "Events": [
    {
      "DateTime: ""
      "Name": "ACCOUNT_OPEN_INITIATED",
      "Type": "ACCOUNT",
      "Category": "INITIATION",
      "Application": { "href": "https://api.publicissapient.com/applications/399appdo-uiisd" }
    }
  ]
}
```

|Event Property|Value|
|--------|-----|
|Name|ACCOUNT_OPEN_INITIATED|
|Type|ACCOUNT|
|Category|INITIATION|
|Application|a link to details about the application|

Triggered when the a banking account opening applciation has been submitted.


# Account Open

(for an existing authenticated customer)

## Get account eligibility

```shell
curl "https://api.publicissapient.com/products?category=accounts" \
  -H "Authorization: Bearer token"
```

> The above command returns an list of account types that the user can open

```json
{
  "_links": {
    "self": { "href": "https://api.publicissapient.com/products?category=accounts" },
    "curie": {
      "name": "ps",
      "href": "https://api.publicissapient.com/rels/{rel}",
      "templated": true
    }
  },
  "_embedded": {
    "Products": [
      {
        "_links": {
          "ps:apply": { "href": "https://api.publicissapient.com/products/12234BAS/apply" }
        },
        "ProductId": "12234BAS",
        "ProductType": "PersonalCurrentAccount",
        "ProductName": "Basic Bank Account",
        "ProductDescription": "",
        "CardImage": "https://publicissapient.com/baas/img/basic-bank-acct.png",
        "OnboardingRequirements": [
          {
            "Title": "Your account",
            "Description": "How you plan to use the youth account",
            "Icon": "https://publicissapient.com/baas/img/about-account.png"           
          }          
        ]
      },
      {
        "_links": {
          "ps:apply": { "href": "https://api.publicissapient.com/accounts/144414YBAS/apply" }
        },
        "ProductId": "144414YBAS",
        "ProductType": "YouthCurrentAccount",
        "ProductName": "Youth Account",
        "ProductDescription": "",
        "CardImage": "https://publicissapient.com/baas/img/basic-bank-acct.png",
        "OnboardingRequirements": [
          {
            "Title": "About you",
            "Description": "Your relationship and applicant details",
            "Icon": "https://publicissapient.com/baas/img/about-you.png"           
          },
          {
            "Title": "Your account",
            "Description": "How you plan to use the youth account",
            "Icon": "https://publicissapient.com/baas/img/about-account.png"           
          },
          {
            "Title": "Your identity",
            "Description": "Checking to make sure the appliant's ID matches their details",
            "Icon": "https://publicissapient.com/baas/img/about-identity.png"                    
          }

        ]
      }
    ]
  }
}
```

1 - Get a list of accounts that this authenticated user can open
2 - initiate account open process (bank determines what the requirements are based on the type of account the user is trying to open)
3 - verify identity (determine what type of document is required for KYC, etc)
4 - initiate a card posting


### HTTP Request

`GET https://api.publicissapient.com/products?category=accounts`

## Retrieve form 

```shell
curl "https://api.publicissapient.com/accounts/144414YBAS/apply" \
  -H "Authorization: Bearer token" \
  -H "Accept: application/prs.hal-forms+json"
```

```json
{
  "_links": {
    "self": { "href": "https://api.publicissapient.com/accounts/144414YBAS/apply" },
    "curie": {
      "name": "ps",
      "href": "https://api.publicissapient.com/rels/{rel}",
      "templated": true
    }
  },  
  "_templates" : {
    "default" : {
      "title" : "",
      "method" : "POST",
      "_htarget": "https://api.publicissapient.com/accounts/144414YBAS/apply/step1",
      "contentType" : "application/json",
      "properties" : [
        { 
          "name" : "citizen", 
          "prompt" : "Are you a British citizen?", 
          "description": "", 
          "options": {
            "inline" : ["Yes", "No"]
          },
          "maxItems": 1
        },
        { "name": "email", "prompt": "What is your email address?", "description": "", "type": "email", "required": true }
      ]
    }
  }
}
```

An application process may be split into multiple forms so that a dynamic on-boarding process can be followed.

## Submit form

```shell
curl -X POST https://api.publicissapient.com/accounts \
-H 'Content-Type: application/json' \
-H 'Accept: application/hal+json' \
-d '{
  "citizen" : "Yes",
  "email": "ronnie.mitra@publicissapient.com"
}'
```

> The above command submits form details, resulting in ..?

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


