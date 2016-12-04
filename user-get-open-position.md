## Get open positions of a specified user

GET http://api.ubinary.com/trading/affiliate/12345/user/get/open/positions?data=JSON_DATA

where `12345` - is your affiliate id and `JSON_DATA` is like

```C#
{
    string UserId;              // User email or user id
}
```

##### A valid request example

http://api.ubinary.com/trading/affiliate/12345/user/get/open/positions?data={"UserId":"john@ub.com"} 

```json
{
    "UserId": "john@ub.com",
}
```

http://api.ubinary.com/trading/affiliate/12345/user/get/open/positions?data={"UserId":"123456"} 

```json
{
    "UserId": 123456,
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
    Position[] Positions;         // array of open positions
}

enum Direction { Above, Below }

class Position
{
    int PositionId;
    string Asset;
    string ProductName;
    decimal Stake;
    Direction Direction;
    DateTime StartedAt;
    DateTime ExpirationAt;
    decimal OpenRate;
    decimal CloseRate;
    decimal Payout;
    string CloseReason;
}
```

#### Successful response example

```json
{
  "TrackingId": "57.28.63",
  "ErrorCode": "Ok",
  "ErrorMessage": "",
  "Positions": [
    {
      "PositionId": 676449,
      "Asset": "GBPUSD",
      "ProductName": "Sixty seconds",
      "Stake": 40,
      "Direction": "Above",
      "StartedAt": "24-Nov-2014 08:50:04",
      "ExpirationAt": "24-Nov-2014 08:51:04",
      "OpenRate": 1.5061,
      "CloseRate": 0,
      "Payout": 0,
      "CloseReason": null
    }
  ]
}
```


##### Unsuccessful response example

```json
{
  "TrackingId": "37.30.05",
  "ErrorCode": "Failed",
  "ErrorMessage": "User 'john@ub.com' is not registered"
}
```


#### Expectations
None

#### Access restrictions
- White IP list
