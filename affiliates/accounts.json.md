## Users (leads) report

Get all **changed** users between specified dates

GET http://api.ubinary.com/reports/affiliate/AFF_ID/accounts.json?from=FROM_DATE&to=TO_DATE&PagingIndex=PAGING_INDEX

where parameters are

Parameter       | Format                  | Description
----------------|-------------------------|-------------
AFF_ID          | integer                 | Your affiliate ID number
FROM_DATE       | 'yyyy-MM-dd HH:mm:ss'   | Start from this date
FROM_TO         | 'yyyy-MM-dd HH:mm:ss'   | Until this date
PAGING_INDEX    | integer                 | 1 for first request, PagingIndex from a response if its HasMoreData is true
AccountID       | integer                 | Account ID of the user


#### Response

Status | Response body
-------|--------------
200    | JSON_RESPONSE

where `JSON_RESPONSE` is like

```C#
{
    int PagingIndex;            // should be used in a consequent request
    int HasMoreData;            //     if there is more data
    Account[] Accounts;         // an array of retrieved users
}

class Account
{
    DateTime TransactionDate;   // Lead creation date
    string cTag;                // the free Ctag parameter sent with registration API
    int AccountID;              // User id
    string Type;                // 'lead' or 'user' (a user is a lead with one successful login)
    string FirstName;
    string LastName;
    string Email;               // User's email
    string CountryCode;         // User's country code (two letters ISO code)
    string SalesStatus;         // User's sales status (NotConverted, New, NoInterest, PaymentSuccessful, NoAnswer, CallInAWhile, CcClearanceFailed)
}
```

#### Successful request / response example

http://api.ubinary.com/reports/affiliate/12345/accounts.json?from=2014-10-01 00:00:00&to=2014-11-25 00:00:00&PagingIndex=1

```
{
  "HasMoreData": 0,
  "PagingIndex": 8,
  "Accounts": [
    {
      "TransactionDate": "2014-11-08 13:35:42",
      "CTag": null,
      "AccountID": 414098,
      "Type": "user",
      "FirstName": "janet",
      "LastName": "polli",
      "Email": "janetp@example.com",
      "CountryCode": "SA",
      "SalesStatus": "PaymentSuccesful"
    },
    ...
  ]
}
```

#### Paging index sample

*CAUTION:* PagingIndex is not the index of a desired page

In the first request PagingIndex should be 1

http://api.ubinary.com/reports/affiliate/12345/accounts.json?from=2014-10-01 00:00:00&to=2014-11-25 00:00:00&PagingIndex=1

```
{
  "HasMoreData": 1,
  "PagingIndex": 101,
  ...
}
```

Response indicates that there is more data - `HasMoreData` is 1

In the next request use PagingIndex from the response above

http://api.ubinary.com/reports/affiliate/12345/accounts.json?from=2014-10-01 00:00:00&to=2014-11-25 00:00:00&PagingIndex=101

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
