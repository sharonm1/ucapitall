## Get trading options

GET http://api.ubinary.com/trading/affiliate/12345/user/get/trading/options?data=JSON_DATA

where `12345` - is your affiliate id and `JSON_DATA` is like

```C#
{
    string UserId;              // not supported yet
}
```

##### A valid request example

http://api.ubinary.com/trading/affiliate/12345/user/get/trading/options?data={"UserId":""} 

```json
{
    "UserId": ""
}
```


#### Response

Status | Response body
-------|--------------
200    | JSON_RESPONSE

where `JSON_RESPONSE` is like

```C#
{
    string TrackingId;            // Tracking id for troubleshooting
    string ErrorCode;             // "Ok" if request succeeds, short error code if request fails
    string ErrorMessage;          // error description if request fails
    Option[] Options;             // array of asset options
}

class Option
{
    string Symbol;
    Deal[] Deals;
}

class Deal
{
    int DealId;                   // Deal id (to be used in open position request)
    DateTime StartAt;             // deal start date
    DateTime EndAt;               // deal end date
    bool ExpirationIsFixed;       // if true - positions opened on this deal will expire with the deal
                                  //    false - position will expire at now + Duration
    TimeSpan Duration;            // Position duration (if expiration is not fixed)
    decimal PayMatch;             // Percents (stake) payed if positions wins
    decimal PayNoMatch;           // Percents (stake) payed if position losses
    decimal MinStake;             // Minimum stake for this deal
    decimal MaxStake;             // Maximum stake for this deal
}

```

#### Successful response example

```json
{
  "TrackingId": "87.35.06",
  "ErrorCode": "Ok",
  "ErrorMessage": "",
  "Options": [
    {
      "Symbol": "EURUSD",
      "Deals": [
        {
          "DealId": 948504,
          "StartAt": "24-Nov-2014 09:35:00",
          "EndAt": "24-Nov-2014 11:00:00",
          "ExpirationIsFixed": true,
          "Duration": "00:00:00",
          "PayMatch": 75,
          "PayNoMatch": 0,
          "MinStake": 20,
          "MaxStake": 100000
        },
        {
          "DealId": 960885,
          "StartAt": "02-Dec-2014 07:40:00",
          "EndAt": "02-Dec-2014 15:50:00",
          "ExpirationIsFixed": false,
          "Duration": "00:01:00",
          "PayMatch": 75,
          "PayNoMatch": 0,
          "MinStake": 20,
          "MaxStake": 50000
        }
      ]
    }
  ]
}
```


##### Unsuccessful response example

```json
{
  "TrackingId": "37.30.05",
  "ErrorCode": "Failed",
  "ErrorMessage": " Affiliate 111111 has no bot associated with"
}
```


#### Expectations
None

#### Access restrictions
- White IP list
