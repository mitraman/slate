# Transactions

Use the `transactions` endpoint to retrieve a list of transactions associated with an authenticated customer.

## Transactions Data Model

TBD

## Get all transactions

```shell
curl "http://example.com/api/transactions" \
  -H "Authorization: Bearer token"
```

> The above command returns a list of transactions in a JSON collection:

```json
HTTP 200 OK

{
  "_links": {
    "self": { "href": "" },
    "next": { "href": "http://api.publicissapient.com/baas/transactions?from=100821&to=" },
    "prev": { "href": "http://api.publicissapient.com/baas/transactions?" },
  },
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
        "ValueDateTime": "2017-04-05T10:45:22+00:00",
        "TransactionInformation": "Cash from Aubrey",
        "BankTransactionCode": {
          "Code": "ReceivedCreditTransfer",
          "SubCode": "DomesticCreditTransfer"
        },
        "ProprietaryBankTransactionCode": {
          "Code": "Transfer",
          "Issuer": "AlphaBank"
        },
        "Balance": {
          "Amount": {
            "Amount": "230.00",
            "Currency": "GBP"
          },
          "CreditDebitIndicator": "Credit",
          "Type": "InterimBooked"
        }
      }
  ],
  "Meta": {
  } 
}
```

### HTTP Request

`GET http://api.publicissapient.com/transactions`


## Filter the list

Filter the list with query parameters

### HTTP Request

`GET http://api.publicissapient.com/transactions`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
fromDateTime |  | the starting date-time for transactions to list in the response
toDateTime |  | the ending date-time for transactions to list in the response
reference | '' | text to search for in transaction reference data


## Search for a transaction

```shell
curl "http://example.com/api/accounts/22289/balance" \
  -H "Authorization: Bearer token"
```

```shell
curl -X POST https://api.publicissapient.com/transactions/search \
-H 'Content-Type: application/json' \
-d '{
  "start_date": "2018-01-01",
  "end_date": "2018-02-01",
  "reference": "",
  "amount": {
    "min": "10.00",
    "max": "100.00"
  }
}'
```

> The above command returns a list of transactions as an array:

```json
HTTP 200 OK

{
 
}
```


This endpoint retrieves a list of transactions for an authenticated user based on the POSTed search request. 

### HTTP Request

`POST http://api.publicissapient.com/transactions/search`

