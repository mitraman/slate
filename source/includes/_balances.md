# Balances

Use the `balances` endpoint to retrieve with balances associated with an authenticated user's bank accounts

## Balances Data Model

### AccountID 

```
"AccountId": "22289"
```

*string*

A unique and immutable identifier used to identify the account resource. 


### Amount

```
"Amount": {
    "Amount": "1230.00",
    "Currency": "GBP"
}
```

*object*

A monetary amount data object that describes the cash balance available in the account. It includes the following properties:

* Amount - a floating point number with two decimal places
* Currency - a country-code based currency indicator as defined in [ISO-4217](https://www.iso.org/iso-4217-currency-codes.html)


### CreditDebitIndicator

```
"CreditDebitIndicator": "Credit"
```

*enumerated string*

Indicates whether the balance is a credit or a debit balance. Usage: A zero balance is considered to be a credit balance.

Only the following values are supported:
* "Credit"
* "Debit"

### Type

```
"Type": "InterimAvailable"
```

*enumerated string*

Balance type, in a coded form.

Only the following values are supported:
* ClosingAvailable
* ClosingBooked
* ClosingCleared
* Expected
* ForwardAvailable
* Information
* InterimAvailable
* InterimBooked
* InterimCleared
* OpeningAvailable
* OpeningBooked
* OpeningCleared
* PreviouslyClosedBooked


### DateTime

```
"DateTime": "2017-04-05T10:43:07+00:00"
```

*string*

Indicates the date (and time) of the balance in [ISO-8601](https://www.iso.org/iso-8601-date-and-time-format.html) format.


### CreditLine

```
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
```

*array*

Set of elements used to provide details on the credit line. It includes the following properties:

* Included - A boolean value indicating whether or not the credit line is included in the balance of the account. Usage: If not present, credit line is not included in the balance amount of the account.
* Amount - An amount object indicating the amount of money of the credit line.
* Type - Limit type, in a coded form. It may have one of the following values: 'Available', 'Credit', 'Emergency', 'Pre-Agreed', 'Temporary'



## Retrieve the Balance for a specific Bank Account

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

## Retrieve all Account Balances

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
