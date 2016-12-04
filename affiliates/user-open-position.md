## Open position for a specified user

GET http://api.ubinary.com/trading/affiliate/12345/user/open/position?data=JSON_DATA

where `12345` - is your affiliate id and `JSON_DATA` is like

```C#
{
    enum EAboveBelow { Above, Below }

    string SessionKey;          // Returned by a successful login   
    string UserId;              // User email or user id (both are supported)
    string UserPassword;        // User password
    int DealId;                 // A coresponding deal id (from get-trading-options)
    EAboveBelow AboveBelow;     // Position direction should be 'Above' or 'Below'
    decimal Stake;              // Position volume in USD
}
```

##### A valid request example

```json
{
    "SessionKey": "47d8fd5711b84a39a696e5c3b79241f9",
    "UserId": "john@ub.com",
    "UserPassword": "111111",
    "DealId": 948504,
    "AboveBelow": "Above",
    "Stake": 40
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
    int PositionId;               // Id of an successfully opened position
    DateTime ExpirationAt;        // Comment": "Position expiration point
}
```

##### Successful response example

```json
{
  "TrackingId": "74.77.97",
  "ErrorCode": "Ok",
  "ErrorMessage": "",
  "PositionId": 821416,
  "ExpirationAt": "24-Nov-2014 10:08:49"
}
```


##### Unsuccessful response example

```json
{
  "TrackingId": "34.29.31",
  "ErrorCode": "UxError",
  "ErrorMessage": "User 291935 (john@ub.com): login failed; password is wrong",
  "PositionId": 0,
  "ExpirationAt": "01-Jan-0001 00:00:00"
}
```


#### Expectations
- Affiliate is logged in

#### Access restrictions
- White IP list
