# Pots

Flexible expense reporting functionality with extensive filtering capabilities (meniga)

## Generate a report

# Goals

Enable users to set saving goals and motivate customers to reach savings goals with Challenges (meniga)

## Data Model


### Accounts

```
"Accounts": [ "22289" ]
```

*array*

A list of account balance used to calculate this goal

### Name

```
"Name": "Kairav's University Fees"
```

*string*

The name of this goal

### Description

```
"Description": "TBD"
```

*string*

A text description of the goal


### Category

```
"Category": "Education"
```

*string*

TBD

### StartDate

```
"DateTime": "2017-04-05T10:43:07+00:00"
```

*string*

Indicates the starting date (and time) of the goal in [ISO-8601](https://www.iso.org/iso-8601-date-and-time-format.html) format.


### TargetDate

```
"DateTime": "2017-04-05T10:43:07+00:00"
```

*string*

Indicates the target date (and time) of the goal in [ISO-8601](https://www.iso.org/iso-8601-date-and-time-format.html) format.


### TargetAmount

TBD

### CurrentAmount

TBD

### Progress

Percentage progress towards the goal

### EstimatedTargetDate

A calculated estimate of when the savings goal will be met

### GoalStatus

*enumerated string*

### AchievedDate

### History

*array*

An array of time series data that plots the historical progress towards a goal within a time range


 
## Create a new goal

```shell
curl -X POST https://api.publicissapient.com/accounts \
-H 'Content-Type: application/json' \
-d '{
  "name" : "Kairav\'s University Fees",
  "StartDate": "2021-10-05T22:09:09.277Z",
  "TargetDate": "2021-10-05T22:09:09.277Z",
  "TargetAmount": 0      
}'
```

> If succesful, the API resonds with the goal object in JSON form:

```json
{
  "Goals": [
    {
      "GoalId": "99392",
      "AccountId": 0,
      "Name": "Kairav's University Fees",
      "StartDate": "2021-10-05T22:09:09.277Z",
      "TargetDate": "2021-10-05T22:09:09.277Z",
      "TargetAmount": 0,
      "CurrentAmount": 0,
      "RecurringAmount": 0,
      "ExpectedTargetDate": "2021-10-05T22:09:09.277Z",
      "CategoryId": 0,
      "LifeGoalStatus": "OnSchedule"
    }
  ]
}
```

Create a new savings goal

## Retrieve goals

```shell
curl "http://example.com/api/goals" \
  -H "Authorization: Bearer token"
```

> Returns a list of goals associated with the authenticated user:

```json
{
  "Goals": [
    {  
      "GoalId": "99392",
      "AccountId": 0,
      "Name": "Kairav's University Fees",
      "StartDate": "2021-10-05T22:09:09.277Z",
      "TargetDate": "2021-10-05T22:09:09.277Z",
      "TargetAmount": 0,
      "CurrentAmount": 0,
      "RecurringAmount": 0,
      "ExpectedTargetDate": "2021-10-05T22:09:09.277Z",
      "CategoryId": 0,
      "LifeGoalStatus": "OnSchedule",
      "AchievedDate": "2021-10-05T22:09:09.277Z"
    }
  ]
}
```


## Update a goal

## Delete a goal

## Retrieve goal history

```shell
curl "http://example.com/api/goals/388/history" \
  -H "Authorization: Bearer token"
```

> Provided that the goal exists and is retrievable, this command will return a time-series history of goal data:

```json
{
  "History": {
      "StartTime": "",
      "EndTime": "",
      "Transactions": [
        {          
          "AccountId": "22289",          
          "TransactionId": "123",
          "TransactionReference": "Ref 1",
          "Amount": {
            "Amount": "10.00",
            "Currency": "GBP"
          },
          "CreditDebitIndicator": "Credit",
          "Status": "Booked",
          "BookingDateTime": "2017-04-05T10:43:07+00:00",
          "TransactionInformation": "Cash from Aubrey"
        },
        {},
        {}
      ]

  }
}
```



# Budgets

Flexible expense reporting with extensive filtering capabilities (meniga)

## Retrieve budgets

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

## Create a new budget

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

## Update a budget

## Retrieve loan products