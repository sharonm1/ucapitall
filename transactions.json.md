## Transactions report

Get fund transactions between specified dates

GET http://api.ubinary.com/reports/affiliate/AFF_ID/transactions.json?from=FROM_DATE&to=TO_DATE&PagingIndex=PAGING_INDEX


where parameters are

Parameter       | Format                  | Description
----------------|-------------------------|-------------
AFF_ID          | integer                 | Your affiliate ID
FROM_DATE       | 'yyyy-MM-dd HH:mm:ss'   | Start from this date
FROM_TO         | 'yyyy-MM-dd HH:mm:ss'   | Until this date
PAGING_INDEX    | integer                 | 1 for first request, PagingIndex from a response if its HasMoreData is true

#### Response

Status | Response body
-------|--------------
200    | JSON_RESPONSE

where `JSON_RESPONSE` is like

```C#
{
    int PagingIndex;            // should be used in a consequent request
    int HasMoreData;            //     if there is more data
    Transaction[] Transactions; // an array of retrieved transactions
}

class Transaction
{
    string TransactionDate;
    string CTag;
    int AccountID;
    int TransactionID;
    string ActionName;
    double Amount;
    string Coin;
}
```

#### Successful request / response example

http://api.ubinary.com/reports/affiliate/12345/transactions.json?from=2014-10-01 00:00:00&to=2014-11-25 00:00:00&PagingIndex=1

```
{
  "HasMoreData": 0,
  "PagingIndex": 5,
  "Transactions": [
    {
      "TransactionDate": "2014-11-06 13:21:48",
      "CTag": null,
      "AccountID": 413003,
      "TransactionID": 810064,
      "ActionName": "deposit",
      "Amount": 250,
      "Coin": "USD"
    },
    ...
  ]
}
```

#### Paging index sample

*CAUTION:* PagingIndex is not the index of a desired page

In the first request PagingIndex should be 1

http://api.ubinary.com/reports/affiliate/12345/transactions.json?from=2014-10-01 00:00:00&to=2014-11-25 00:00:00&PagingIndex=1

```
{
  "HasMoreData": 1,
  "PagingIndex": 101,
  ...
}
```

Response indicates that there is more data - `HasMoreData` is 1

In the next request use PagingIndex from the response above

http://api.ubinary.com/reports/affiliate/12345/transactions.json?from=2014-10-01 00:00:00&to=2014-11-25 00:00:00&PagingIndex=101

```
{
  "HasMoreData": 0,
  "PagingIndex": 154,
  ...
}
```

Response indicates that there is no more data - `HasMoreData` is 0

#### Error response sample

```
{
  "Error": "Affiliate id 12345 is not registered"
}
```

#### Expectations
None

#### Access restrictions
- White IP list

